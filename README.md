android-awesome-libraries
=========================

Index
---

- [Support](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#support)
- [Network](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#network)
- [Rest Client](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#rest-client)
- [Object Serialization](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#object-serialization)
- [Network Image Handling](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#network-image-handling)
- [Event Pub/Sub](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#event-pubsub)
- [Utility](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#utility)
- [DI](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#di)
- [View Model Binding](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#view-model-binding)
- [UI](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#ui)
- [Album Handling](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#album-handling)
- [Rx](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#rx)
- [Testing](https://github.com/kaiinui/android-awesome-libraries/blob/master/README.md#testing)

Support
---

- [Android Device Compatibility](https://github.com/mixi-inc/Android-Device-Compatibility) - Compatibility package project for android device difference.

- Android Support Annotations

```java
private void displayName(@NonNull String name) {
  // name can not be null
}
```

```java
private void receiveDrawableRes(@DrawableRes int resId) {
  // resId must be Drawable Resource ID
}
```

- [Retrolabmda](https://github.com/orfjackal/retrolambda) - lambda suppor for android!

```java
mButton.setOnClickListener((View v) -> {
    // do something here
});
```

- [icepick](https://github.com/frankiesardo/icepick)

```java
@Icicle String username; // This will be automatically saved and restored

@Override public void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);
  Icepick.restoreInstanceState(this, savedInstanceState);
}

@Override public void onSaveInstanceState(Bundle outState) {
  super.onSaveInstanceState(outState);
  Icepick.saveInstanceState(this, outState);
}
```

Network
---

- [Volley](https://android.googlesource.com/platform/frameworks/volley)

```java
RequestQueue queue = Volley.newRequestQueue(this);
String url = "SOMEURL";

JsonObjectRequest jsObjRequest = new JsonObjectRequest(Request.Method.GET, url, null, new Response.Listener<JSONObject>() {
  @Override
  public void onResponse(JSONObject response) {
    // TODO
  }
}, new Response.ErrorListener() {
  @Override
  public void onErrorResponse(VolleyError error) {
    // TODO
  }
});

queue.add(jsObjRequest);
```

REST Client
---

- [Retrofit](http://square.github.io/retrofit/)

```java
public interface GitHubService {
  @GET("/users/{user}/repos")
  List<Repo> listRepos(@Path("user") String user);
}
```

Object Serialization
---

- [Gson](https://code.google.com/p/google-gson/)

```java
BagOfPrimitives obj = new BagOfPrimitives();
Gson gson = new Gson();
String json = gson.toJson(obj);  
```

Network Image Handling
---

- [Picasso](http://square.github.io/picasso/)

```java
Picasso.with(context).load("http://i.imgur.com/DvpvklR.png").into(imageView);
```

- [Universal Image Loader](https://github.com/nostra13/Android-Universal-Image-Loader)

```java
// Load image, decode it to Bitmap and display Bitmap in ImageView (or any other view 
//  which implements ImageAware interface)
imageLoader.displayImage(imageUri, imageView);
```

##### really configurable!

```java
// DON'T COPY THIS CODE TO YOUR PROJECT! This is just example of ALL options using.
// See the sample project how to use ImageLoader correctly.
DisplayImageOptions options = new DisplayImageOptions.Builder()
        .showImageOnLoading(R.drawable.ic_stub) // resource or drawable
        .showImageForEmptyUri(R.drawable.ic_empty) // resource or drawable
        .showImageOnFail(R.drawable.ic_error) // resource or drawable
        .resetViewBeforeLoading(false)  // default
        .delayBeforeLoading(1000)
        .cacheInMemory(false) // default
        .cacheOnDisk(false) // default
        .preProcessor(...)
        .postProcessor(...)
        .extraForDownloader(...)
        .considerExifParams(false) // default
        .imageScaleType(ImageScaleType.IN_SAMPLE_POWER_OF_2) // default
        .bitmapConfig(Bitmap.Config.ARGB_8888) // default
        .decodingOptions(...)
        .displayer(new SimpleBitmapDisplayer()) // default
        .handler(new Handler()) // default
        .build();
```

Event Pub/Sub
---

- [Otto](http://square.github.io/otto/)

```java
bus.post(new AnswerAvailableEvent(42));
```

```java
@Subscribe public void answerAvailable(AnswerAvailableEvent event) {
    // TODO: React to the event somehow!
}
```

- [EventBus](https://github.com/greenrobot/EventBus)

```java
eventBus.post(event);
```

```java
eventBus.register(this);
public void onEvent(AnyEventType event) {
    // TODO: React to the event!
}
```

Utility
---

- [Android Priority Job Queue](https://github.com/path/android-priority-jobqueue)

```java
public void onSendClick() {
    final String status = editText.getText().toString();
    if(status.trim().length() > 0) {
      jobManager.addJobInBackground(new PostTweetJob(status));
      editText.setText("");
    }
}
```

- [ObjectCache](https://github.com/iainconnor/ObjectCache)

```java
MyObject myObject = new MyObject("foo");
cacheManager.put("myKey", myObject);
```

DI
---

- [ButterKnife](https://github.com/JakeWharton/butterknife)

```java
@InjectView(R.id.user) EditText username;
@InjectView(R.id.pass) EditText password;

@OnClick(R.id.submit) void submit() {
  // TODO call server...
}
```

- [Dagger](http://square.github.io/dagger/)

```java
@Inject
Thermosiphon(Heater heater) {
  this.heater = heater;
}
```

View Model Binding
---

- [android-binding](https://github.com/gueei/AndroidBinding)

```java
public StringObservable message = new StringObservable();
...
message.set("Hello MVVM!"); // will change the model and view
```

UI
--

- [PhotoView](https://github.com/chrisbanes/PhotoView) - ImageView for Android that supports zooming, by various touch gestures.

![](https://camo.githubusercontent.com/cf5bfb6d896604aa9156e3e1beee89e0754de7db/68747470733a2f2f7261772e6769746875622e636f6d2f636872697362616e65732f50686f746f566965772f6d61737465722f6865616465725f677261706869632e706e67)

- [cardslib](https://github.com/gabrielemariotti/cardslib)

![](https://github.com/gabrielemariotti/cardslib/raw/master/demo/images/screen.png)

- [Android-Rate](https://github.com/hotchemi/Android-Rate)

![](https://camo.githubusercontent.com/39978e2edcf111ea1fa024ed66558da961926694/687474703a2f2f6769667a6f2e6e65742f4249356532714d4a5669302e676966)

Album handling
---

- [DeviceAlbums](https://github.com/nohana/DeviceAlbums) (Compatibility library for dealing with various device photo albums.) 
- [Laevatein](https://github.com/nohana/Laevatein)

![](https://raw.githubusercontent.com/nohana/Laevatein/master/documents/ss-1.png)

- RoboGuice

Rx
---

- [RxJava](https://github.com/Netflix/RxJava)

```java
Subscription sub = Observable.from(1, 2, 3, 4, 5)
    .subscribeOn(Schedulers.newThread())
    .observeOn(AndroidSchedulers.mainThread())
    .subscribe(observer);
```

Testing
---

### Unit

- JUnit
- [Robospock](http://robospock.org/)

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

- [AssertJ](http://joel-costigliola.github.io/assertj/)

```java
assertThat(frodo.getName()).isEqualTo("Frodo");
assertThat(frodo).isNotEqualTo(sauron)
                 .isIn(fellowshipOfTheRing);
assertThat(sauron).isNotIn(fellowshipOfTheRing);
```

### Mock

- [Mockito](https://code.google.com/p/mockito/)

```java
LinkedList mockedList = mock(LinkedList.class);
when(mockedList.get(0)).thenReturn("first");
when(mockedList.get(1)).thenThrow(new RuntimeException());
```

### UI

- Appium
- Espresso

