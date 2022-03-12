> Thinking

```
LifecycleOwner # getLifecycle
Lifecycle
	addObserver removeObserver # LifecycleObserver
	getCurrentState # Lifecycle.State
Lifecycle.State
	isAtLeast
	INITIALIZED
	CREATED
	STARTED
	RESUMED
	DESTROYED
Lifecycle.Event #
	ON_ANY
	ON_CREATE ON_DESTROY
	ON_START ON_STOP
	ON_RESUME ON_PAUSE
LifecycleObserver
	LifecycleEventObserver # onStateChanged
	FullLifecycleObserver
		onCreate onDestroy
		onStart onStop
		onResume onPause

ComponentActivity
	mLifecycleRegistry
ReportFragment

SafeIterableMap<K, V>
SafeIterableMap<K, V> implements Iterable<Map.Entry<K, V>>

-Entry<K, V> mStart
-Entry<K, V> mEnd
-WeakHashMap<SupportRemove<K, V>, Boolean> mIterators

ListIterator<K, V> implements Iterator<Map.Entry<K, V>>, SupportRemove<K, V>
Entry<K, V> mExpectedEnd
Entry<K, V> mNext

AscendingIterator<K, V> extends ListIterator<K, V>
DescendingIterator<K, V> extends ListIterator<K, V>
IteratorWithAdditions implements Iterator<Map.Entry<K, V>>, SupportRemove<K, V>

SupportRemove<K, V>
Entry<K, V> implements Map.Entry<K, V>
```

> Memory

```
androidx.lifecycle:lifecycle-common:2.2.0
androidx.lifecycle:lifecycle-common-java8:2.2.0
androidx.lifecycle:lifecycle-compiler:2.2.0
androidx.lifecycle:lifecycle-extensions:2.2.0
androidx.lifecycle:lifecycle-livedata:2.2.0
androidx.lifecycle:lifecycle-livedata-core:2.2.0
androidx.lifecycle:lifecycle-reactivestreams:2.2.0
androidx.lifecycle:lifecycle-runtime:2.2.0
androidx.lifecycle:lifecycle-viewmodel:2.2.0
androidx.lifecycle:lifecycle-viewmodel-savedstate:2.2.0

android.arch.lifecycle:common
android.arch.lifecycle:common-java8
android.arch.lifecycle:compiler
android.arch.lifecycle:extensions
android.arch.lifecycle:livedata
android.arch.lifecycle:livedata-core
android.arch.lifecycle:reactivestreams
android.arch.lifecycle:runtime
android.arch.lifecycle:viewmodel
无 viewmodel-savedstate
```

