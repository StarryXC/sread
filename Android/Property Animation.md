> Thinking

```
Animator # 属性动画
	AnimatorSet
	ValueAnimator
		ObjectAnimator
		TimeAnimator
Keyframe
PropertyValuesHolder

Animator.AnimatorListener
Animator.AnimatorPauseListener
ValueAnimator.AnimatorUpdateListener

<set>
	android:ordering # sequentially
<animator> # ValueAnimator
	android:duration
	android:interpolator # @android:interpolator/linear
	android:repeatCount # infinite
	android:repeatMode # restart
	android:startOffset # 0
	android:valueFrom android:valueTo
	android:valueType # colorType
<objectAnimator>
	android:propertyName
	android:duration
	android:valueFrom android:valueTo
	android:valueType # intType
	android:startOffset
	android:repeatMode # restart
	android:repeatCount # infinite
	android:interpolator # @android:interpolator/linear
	android:pathData # 1,2,2,3,5
	android:propertyXName android:propertyYName
<propertyValuesHolder>
	android:valueFrom android:valueTo
	android:valueType
	android:propertyName

AnimatorSet
	playTogether
AnimatorInflater
	loadAnimator
Animator
	addListener # Animator.AnimatorListener onAnimationStart onAnimationEnd onAnimationCancel onAnimationRepeat
	addPauseListener # Animator.AnimatorPauseListener onAnimationPause onAnimationResume
ValueAnimator
	ofInt
	ofPropertyValuesHolder
	addUpdateListener # ValueAnimator.AnimatorUpdateListener onAnimationUpdate
```

> Memory

```

```

