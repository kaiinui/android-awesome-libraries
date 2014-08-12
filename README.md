android-awesome-libraries
=========================

Index
---

- [Support](https://github.com/kaiinui/android-awesome-libraries#support)
- [Network](https://github.com/kaiinui/android-awesome-libraries#network)
- [Rest Client](https://github.com/kaiinui/android-awesome-libraries#rest-client)
- [Object Serialization](https://github.com/kaiinui/android-awesome-libraries#object-serialization)
- [Database](https://github.com/kaiinui/android-awesome-libraries#database)
- [Network Image Handling](https://github.com/kaiinui/android-awesome-libraries#network-image-handling)
- [Event Pub/Sub](https://github.com/kaiinui/android-awesome-libraries#event-pubsub)
- [Utility](https://github.com/kaiinui/android-awesome-libraries#utility)
- [DI](https://github.com/kaiinui/android-awesome-libraries#di)
- [View Model Binding](https://github.com/kaiinui/android-awesome-libraries#view-model-binding)
- [UI](https://github.com/kaiinui/android-awesome-libraries#ui)
- [Album Handling](https://github.com/kaiinui/android-awesome-libraries#album-handling)
- [Rx](https://github.com/kaiinui/android-awesome-libraries#rx)
- [Promise](https://github.com/kaiinui/android-awesome-libraries#promise)
- [Debug Utilitiy](https://github.com/kaiinui/android-awesome-libraries#debug-utility)
- [Gradle Plugin](https://github.com/kaiinui/android-awesome-libraries#gradle-plugin)
- [Testing](https://github.com/kaiinui/android-awesome-libraries#testing)

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

- [icepick](https://github.com/frankiesardo/icepick) - Android Instance State made easy

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

- [Michelangelo](https://github.com/RomainPiel/Michelangelo) - Layout inflation library for Android based on annotations

```java
@InflateLayout(R.layout.custom_view)
public class MyCustomView extends FrameLayout {

    public MyCustomView(Context context) {
        super(context);
    }

    @AfterInflate
    public void updateTextView() {
        ((TextView) findViewById(R.id.my_text_view)).setText("hey!");
    }
}
```

- [AndroidAnnotations](http://androidannotations.org/)

```java
@Background
void someBackgroundWork(String aParam, long anotherParam) {
    [...]
}
```

```java
@UiThread
void doInUiThread(String aParam, long anotherParam) {
    [...]
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

- [ion](https://github.com/koush/ion)

```java
Ion.with(context)
.load("http://example.com/thing.json")
.asJsonObject()
.setCallback(new FutureCallback<JsonObject>() {
   @Override
    public void onCompleted(Exception e, JsonObject result) {
        // do stuff with the result or error
    }
});
```

- [okhttp](https://github.com/square/okhttp) - An **HTTP+SPDY** client for Android and Java applications

```java
OkHttpClient client = new OkHttpClient();

String run(String url) throws IOException {
  Request request = new Request.Builder()
      .url(url)
      .build();

  Response response = client.newCall(request).execute();
  return response.body().string();
}
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

Database
---

- [ActiveAndroid](https://github.com/pardom/ActiveAndroid)

```java
Category restaurants = new Category();
restaurants.name = "Restaurants";
restaurants.save();
```

- [GreenDAO](https://github.com/greenrobot/greenDAO)

```java
List joes = userDao.queryBuilder()
  .where(Properties.FirstName.eq("Joe"))
  .orderAsc(Properties.LastName)
  .list();
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

- [Routable](https://github.com/usepropeller/routable-android) - routes.rb for Android

```java
Router.sharedRouter().map("users/:id", UserActivity.class);
Router.sharedRouter().map("users/new/:name/:zip", NewUserActivity.class);
```

```java
Router.sharedRouter().open("users/16");
Router.sharedRouter().open("users/new/Clay/94303");
```

- [GAlette](https://github.com/uPhyca/GAlette) - Tracking events with Google Analytics by annotations

```java
@SendEvent(category = "HelloWorld", action = "sayHello", label="%1$s")
String sayHello (String name) {
  return format("Hello, %s.", name);
}
```

- [Paraphrase](https://github.com/JakeWharton/paraphrase) - compile-safe format string builders.

```xml
<string name="greeting">Hello, {other_name}! My name is {my_name}.</string>
```

```java
CharSequence greeting = Phrase.greeting()
    .other_name("GitHub user")
    .my_name("Jake Wharton")
    .build(this);
```

- [esperandro](https://github.com/dkunzler/esperandro) - Easy SharedPreference Engine foR ANDROid

```java
String superFancyPreference = preferences.superFancyPreferenceKey()
preferences.superFancyPreferenceKey(superFancyPreference)
```

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

- [GPUImage for Android](https://github.com/CyberAgent/android-gpuimage#gpuimage-for-android)

```java
mGPUImage = new GPUImage(this);
mGPUImage.setGLSurfaceView((GLSurfaceView) findViewById(R.id.surfaceView));
mGPUImage.setImage(imageUri); // this loads image on the current thread, should be run in a thread
mGPUImage.setFilter(new GPUImageSepiaFilter());
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

- [android-binding](https://github.com/gueei/AndroidBinding) - MVVM for Android

```java
public StringObservable message = new StringObservable();
...
message.set("Hello MVVM!"); // will change the model and view
```

UI
--

- [SuperToasts](https://github.com/JohnPersano/SuperToasts)

![](https://camo.githubusercontent.com/b52711b589229453cde3c15cebc921285f01d9b8/687474703a2f2f69313031362e70686f746f6275636b65742e636f6d2f616c62756d732f61663238342f547572626f70776e65642f7375706572746f617374735f67726f75705f73637265656e73686f745f74776f2e706e67)

- [PhotoView](https://github.com/chrisbanes/PhotoView) - ImageView for Android that supports zooming, by various touch gestures.

![](https://camo.githubusercontent.com/cf5bfb6d896604aa9156e3e1beee89e0754de7db/68747470733a2f2f7261772e6769746875622e636f6d2f636872697362616e65732f50686f746f566965772f6d61737465722f6865616465725f677261706869632e706e67)

- [SlidingMenu](https://github.com/jfeinstein10/SlidingMenu)

![](https://lh4.ggpht.com/MSBdACpt_6MmrSiGA5f2GrBfmHVCQP4j3n1TUNdN8gKjOfsOqyEe6ELnLXmJi4gRMA=h900-rw)

- [cardslib](https://github.com/gabrielemariotti/cardslib)

![](https://github.com/gabrielemariotti/cardslib/raw/master/demo/images/screen.png)

- [CardsUI for Android](https://github.com/Androguide/cardsui-for-android)

![](https://camo.githubusercontent.com/2c232fa27583ffa8e6cdf34c31509d1f0bbae3b4/687474703a2f2f696d616765736861636b2e75732f612f696d673833372f313336352f636172647367656e312e706e67)

- [Android-Rate](https://github.com/hotchemi/Android-Rate)

![](https://camo.githubusercontent.com/39978e2edcf111ea1fa024ed66558da961926694/687474703a2f2f6769667a6f2e6e65742f4249356532714d4a5669302e676966)

- [GlassActionBar](https://github.com/ManuelPeinado/GlassActionBar)

![](https://camo.githubusercontent.com/01c80fb941f2ba07f6d9d26d80dd4792a79127d4/68747470733a2f2f7261772e6769746875622e636f6d2f4d616e75656c5065696e61646f2f476c617373416374696f6e4261722f6d61737465722f6172742f726561646d655f7069632e706e67)

- [emojicon](https://github.com/rockerhieu/emojicon)

![](https://github.com/rockerhieu/emojicon/raw/master/images/sample.jpg)

- [IonIconView](https://github.com/MarsVard/IonIconView)

![](https://camo.githubusercontent.com/b34ffde14cb738fb283300fe5694e800e22ac783/68747470733a2f2f7261772e6769746875622e636f6d2f4d617273566172642f496f6e49636f6e566965772f6d61737465722f66616e637961642e706e67)

- [ExtendedCalendarView](https://github.com/tyczj/ExtendedCalendarView)

![](https://raw.githubusercontent.com/tyczj/ExtendedCalendarView/master/ExtendedCalendarView/Screenshot_2014-04-04-18-11-16.png)

- [StickyListHeaders](https://github.com/emilsjolander/StickyListHeaders)

![](https://github.com/emilsjolander/StickyListHeaders/raw/master/demo.gif)

- [StickyGridHeaders](https://github.com/TonicArtos/StickyGridHeaders)

![](https://camo.githubusercontent.com/90b57e9383704c400706545225d439e057c6fcc0/687474703a2f2f342e62702e626c6f6773706f742e636f6d2f2d535f4262685758367754592f55517057306377554745492f41414141414141414776552f7a7a4a586a2d50635662592f73313630302f73637265656e2d6c616e6473636170652d736d616c6c65722e706e67)

- [Android Staggered Grid](https://github.com/etsy/AndroidStaggeredGrid)

![](https://camo.githubusercontent.com/a243ad5c2788730c40fc1d348e5ed85adb59c484/687474703a2f2f662e636c2e6c792f6974656d732f327a31423059304d3047304f326b316c334a30332f5472656e64696e672e706e67)

- [JazzyViewPager](https://github.com/jfeinstein10/JazzyViewPager)

- [Android ViewPagerIndicator](https://github.com/JakeWharton/Android-ViewPagerIndicator)

![](https://camo.githubusercontent.com/240ee2f3ebda5f20f73a5750c192a28743227816/68747470733a2f2f7261772e6769746875622e636f6d2f4a616b6557686172746f6e2f416e64726f69642d566965775061676572496e64696361746f722f6d61737465722f73616d706c652f73637265656e732e706e67)

- [RoudedImageView](https://github.com/vinc3m1/RoundedImageView)

![](https://camo.githubusercontent.com/ed1e075be6ed97fa9091d3702e9b96d3e85b7a35/68747470733a2f2f7261772e6769746875622e636f6d2f6d616b6572616d656e2f526f756e646564496d616765566965772f6d61737465722f73637265656e73686f742e706e67)

- [Enhanced ListView](https://github.com/timroes/EnhancedListView)

![](https://lh4.ggpht.com/0XgESm3N-SktOxUhmv4z_hxqkYqBWJJsiVVMS56XSDjmyZVUeXNr9Qe9c8KNF18iIfo=h310-rw)

- [Android Sliding Up Panel](https://github.com/umano/AndroidSlidingUpPanel)

![](https://camo.githubusercontent.com/834cfd81ce764457db69dc023e1bd0adf0a8d00d/68747470733a2f2f7261772e6769746875622e636f6d2f756d616e6f2f416e64726f6964536c6964696e67557050616e656c44656d6f2f6d61737465722f736c6964696e67757070616e656c2e706e67)

- [CWAC TouchListView](https://github.com/commonsguy/cwac-touchlist) - A Drag-and-Drop Capable ListView

- [AdapterViewAnimator](https://github.com/SimonVT/adapterviewanimator)

```java
AdapterViewAnimator animator = new AdapterViewAnimator(adapterView);
data.add(item);
adapter.notifyDataSetChanged();
animator.animate();
```

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

Promise
---

- [JDeffered](https://github.com/jdeferred/jdeferred)

```java
Deferred deferred = new DeferredObject();
Promise promise = deferred.promise();
promise.done(new DoneCallback() {
  public void onDone(Object result) {
    ...
  }
}).fail(new FailCallback() {
  public void onFail(Object rejection) {
    ...
  }
}).progress(new ProgressCallback() {
  public void onProgress(Object progress) {
    ...
  }
}).always(new AlwaysCallback() {
  public void onAlways(State state, Object result, Object rejection) {
    ...
  }
});
```

Debug Utility
---

- [Hugo](https://github.com/JakeWharton/hugo)

```java
@DebugLog
public String getName(String first, String last) {
  SystemClock.sleep(15); // Don't ever really do this!
  return first + " " + last;
}
```

- [scalpel](https://github.com/JakeWharton/scalpel)

![](https://github.com/JakeWharton/scalpel/raw/master/images/sample.gif)

Gradle Plugin
---

- [Gradle Android AspectJ Plugin](https://github.com/uPhyca/gradle-android-aspectj-plugin)

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

- [AssertJ-Android](https://github.com/square/assertj-android)

```java
assertThat(frodo.getName()).isEqualTo("Frodo");
assertThat(frodo).isNotEqualTo(sauron)
                 .isIn(fellowshipOfTheRing);
assertThat(sauron).isNotIn(fellowshipOfTheRing);
```

### Fixture

- [RobotGirl](https://github.com/rejasupotaro/RobotGirl)

```java
Factory.define(
        // This will guess the User class
        new Definition(User.class) {
            @Override
            public Bundle set(Bundle attrs) {
                attrs.putString("name", "John");
                attrs.putBoolean("admin", false);
                return attrs;
            }
        // This will use the User class (Adming would have been guessed)
        }, new Definition(User.class, "admin") {
            @Override
            public Bundle set(Bundle attrs) {
                attrs.putString("name", "Admin");
                attrs.putBoolean("admin", true);
                return attrs;
            }
        });
```

### Mock

- [Mockito](https://code.google.com/p/mockito/)

```java
LinkedList mockedList = mock(LinkedList.class);
when(mockedList.get(0)).thenReturn("first");
when(mockedList.get(1)).thenThrow(new RuntimeException());
```

### UI Test

- [Appium](http://appium.io/)

- [Espresso](https://code.google.com/p/android-test-kit/wiki/Espresso)

```java
public void testSayHello() {
  onView(withId(R.id.name_field))
    .perform(typeText("Steve"));
  onView(withId(R.id.greet_button))
    .perform(click());
  onView(withText("Hello Steve!"))
    .check(matches(isDisplayed()));
}
```

Contribution
===

Just fork & edit & send pull-request on GitHub!

####Policy

1. Official Website over GitHub Repository for links.
2. Should put codes that reflects the library.
3. For UI libraries, put demonstorations.

And I am considering to ...

1. Put reference links for each libraries.
2. Separate pages for each categories.
3. Separate UI categories.

####Maintainer

kaiinui (https://github.com/kaiinui)
