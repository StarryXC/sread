> Thinking

```
Animation 补间动画
	TranslateAnimation 平移
	RotateAnimation 旋转
	AlphaAnimation 渐变
	ScaleAnimation 缩放
	AnimationSet
AnimationDrawable 帧动画 res/drawable/
LayoutAnimationController
	GridLayoutAnimationController
PropertyValuesHolder
TypeEvaluator
	IntEvaluator IntArrayEvaluator
	FloatEvaluator FloatArrayEvaluator
	ArgbEvaluator
	PointFEvaluator RectEvaluator
TimeInterpolator
	Interpolator # 定义动画变化速率
BaseInterpolator
	LinearInterpolator # @android:anim/linear_interpolator 匀速
	DecelerateInterpolator
	AccelerateInterpolator
	AccelerateDecelerateInterpolator # @android:anim/accelerate_decelerate_interpolator 先加速后减速
	OvershootInterpolator AnticipateOvershootInterpolator
	BounceInterpolator @android:anim/bounce_interpolator







```

> Memory

```
<set> # anim.xml
	android:shareInterpolator
	android:duration # 动画时长，单位秒
	android:interpolator # 插值器 @android:anim/linear_interpolator
<translate> # singleable
	android:fromXDelta android:toXDelta # 100%p -100%p
	android:fromYDelta android:toYDelta
	android:duration # 200 毫秒
<alpha> # singleable
	android:fromAlpha android:toAlpha # 0.0~1.0
	android:duration
<scale> # singleable
	android:fromXScale android:toXScale # 0.9 1
	android:fromYScale android:toYScale
	android:pivotX android:pivotY # 50%
	android:duration
<rotate> # singleable
	android:fromDegrees android:toDegrees # 45~90
	android:pivotX android:pivotY # 0.5

<layoutAnimation>
	android:delay # 0.5
	android:animationOrder # random
	android:animation # 动画资源

<accelerateInterpolator> # AccelerateInterpolator @android:anim/accelerate_interpolator
	android:factor # 1.5
	加速
<anticipateInterpolator> # AnticipateInterpolator @android:anim/anticipate_interpolator
	android:tension # 1.5
<anticipateOvershootInterpolator> # AnticipateOvershootInterpolator @android:anim/anticipate_overshoot_interpolator
	android:tension # 1.5
	android:extraTension # 1.5
<cycleInterpolator> # CycleInterpolator @android:anim/cycle_interpolator
	android:cycles # 5
	速率正弦曲线变化
<decelerateInterpolator> # DecelerateInterpolator @android:anim/decelerate_interpolator
	android:factor # 1.5
	减速
<overshootInterpolator> # OvershootInterpolator @android:anim/overshoot_interpolator
	android:tension="1.5

AnimationUtils
	loadAnimation
Animation
	setAnimationListener # Animation.AnimationListener onAnimationStart onAnimationEnd onAnimationRepeat
AnimationSet
	addAnimation
ViewPropertyAnimator # view.animate()
	x # x 是相对父控件
	translationX # translationX 是相对自己
	setDuration
	start
```

