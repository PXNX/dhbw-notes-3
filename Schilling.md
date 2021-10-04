## Allgemein
### VS-Code shortcuts
|shortcut|action|
|---|---|
|<kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>p</kbd> und dann java clean language server oder so eingeben|wenn was rot ist|
|<kbd>shift</kbd> + <kbd>alt</kbd> + <kbd>f</kbd>|pretty print|
---
## Aufbau Spring
* service
* controller
* repository
---
## Dependency Injection
* PA>> inversion of control>> entkoppelung
* set methode statt instanziierungin konstruktor - wir machen es aber via beans
* implementierung mit qconroller oder subklasse annotieren
* in der kalsse in die es dann rein soll @autowired an klassenattribut ran - besser wäre es bei konstruktor (best practice - nur bei Anwendung, nicht bei Test)
---
## Testing
* PA>> Integrationtest, nicht nur Unit Test??
* annotation @springboottest und @autowired
* @mockbean für erstellung leerer hülle eines intefaces
* gleiche ordnerstruktur
* @BeforeEach, @AfterEach, @BeforeAll, @AfterAll um Zustände nach und vor durchläufen zu erstellen
### Statisch
``` java
@Test
public void shouldSuccessfullyDoSomething(){
String parameter1 = "someText";
String parameter2 = "pizza";
String erwartetesResultat = "someText loves pizza!"; // variable sollte lieber expect heißen ;)
assertEquals(erwartetesResultat, greetingService.methode(parameter1,parameter2));
}
```

### Parametrisiert
``` java
@Test
@CsvSource({"paramter1,parameter2,'erwartetesResu,ltat'","aaaparameter1,aaaparameter2,'aaaerwartete,sResultat'"}) // verwendung ' da , es trennen würde
public void shouldSuccessfullyDoSomething(String parameter1, String parameter2,String expect){
String result = greetingService.methode(parameter1,parameter2);
assertEquals(expect, result);
}
```

## test doubles
* fake: alternative implementierung, aber bräuchte viel aufwand
* annotation @mockbean statt @autowired - bspw. wenn man den Controller testet und Service gemockt werden soll
### mock
* automatische generierung
* fokus auf aufruf
* gibt standardwerte zurück (Boolean false, Integer 0, Object null)
* ```verify(quelle, {anzahl der aufrufe}).aufgerufeneMethode(parameter);```
* als paramter bspw. ```anyString()```, also egal welcher string
``` java
@Autowired
Controller controller;

@MockBean
Service service;

@Test
public void shouldBlaBla(){
String parameter1 = "Shrek";

//verhalten des zu mockendne services spezifizieren
when(service.methode(parameter1)).thenReturn("Shrek liebt pizza");

String result = controller.methode(parameter1);
assertEquals("Shrek liebt pizza",result);
}
```

### stub
* fokus auf ergebnis
* semi-automatische generierung
* wir können verhalten anpassen (somit keine standardwerte)
* bei methoden mit rückgabewert: ```when(aufzurufendeMethode()).thenReturn(...);```
* ohne rückgabewert: do--> when
---
