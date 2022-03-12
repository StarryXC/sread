> Thinking

```
Room
```

> Memory

```
https://github.com/ReactiveX/RxJava
https://github.com/ReactiveX/RxAndroid

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
    .map { coinTypeBean -> coinTypeBean.mark.replace("_", "/").toUpperCase() }
    .distinct()
    .toList()
    .subscribe { strings, _ ->
    }

```

