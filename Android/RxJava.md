> Thinking

```
ObservableSource
    Observable
Publisher
    Flowable
SingleSource
    Single
```

> Memory

```
https://github.com/ReactiveX/RxJava
https://github.com/ReactiveX/RxAndroid
// 2.2.21
implementation 'io.reactivex.rxjava2:rxjava:2.1.3'
implementation 'io.reactivex.rxjava2:rxandroid:2.1.1'

背压
subscribe = Flowable.interval(0, 5, TimeUnit.SECONDS)
.onBackpressureDrop()
.subscribe {

Disposable # dispose
ObservableSource
Observable # just iterable map flatMap filter zipWith toList subscribe materialize subscribeOn observeOn
Schedulers # io computation newThread from
AndroidSchedulers # mainThread
Function # apply
Consumer # accept
Predicate # test
Observer # next error complete subscribe
Subscriber # next error complete subscribe
ObservableOnSubscribe # subscribe
Emitter # next error complete
ObservableEmitter # disposed serialize cancellable
Cancellable # cancel
Action # run
Function # 3 4 5 6 7 8 9 | apply

disposable = Flowable.fromIterable(coinTypeBeans)

Flowable flowable = Flowable.fromIterable(new ArrayList<>());

Observable<String> observable = Observable.just("");
observable.map((Function<String, String>) s -> null); observable.map(new Function<String, String>() {
    @Override
    public String apply(@NonNull String s) throws Exception { return null; }
});
observable.distinct();
Single<List<String>> listSingle = observable.toList();
observable.observeOn(Schedulers.io());
observable.subscribe(s -> { }); observable.subscribe(new Consumer<String>() {
    @Override
    public void accept(String s) throws Exception { }
});




```

