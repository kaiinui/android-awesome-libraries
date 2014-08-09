android-awesome-libraries
=========================

Support
---

- Android Support Annotations

DI
---

- ButterKnife https://github.com/JakeWharton/butterknife

```java
@InjectView(R.id.user) EditText username;
@InjectView(R.id.pass) EditText password;

@OnClick(R.id.submit) void submit() {
  // TODO call server...
}
```

- Dagger http://square.github.io/dagger/

```java
@Inject
Thermosiphon(Heater heater) {
  this.heater = heater;
}
```

- RoboGuice

Testing
---

### Unit

- JUnit
- Robospock http://robospock.org/

```groovy
def "should display hello text"() {
    given:
    def textView = new TextView(Robolectric.application)

    and:
    def hello = "Hello"

    when:
    textView.setText(hello)

    then:
    textView.getText() == hello
}
        
```

### Assert

- AssertJ http://joel-costigliola.github.io/assertj/

```java
assertThat(frodo.getName()).isEqualTo("Frodo");
assertThat(frodo).isNotEqualTo(sauron)
                 .isIn(fellowshipOfTheRing);
assertThat(sauron).isNotIn(fellowshipOfTheRing);
```

### Mock

- Mockito https://code.google.com/p/mockito/

```java
LinkedList mockedList = mock(LinkedList.class);
when(mockedList.get(0)).thenReturn("first");
when(mockedList.get(1)).thenThrow(new RuntimeException());
```

### UI

- Appium
- Espresso

