> Thinking

```
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


Animator
    AnimatorSet
    ValueAnimator
        ObjectAnimator
        TimeAnimator
AnimatorInflater

Keyframe
PropertyValuesHolder
```

> Memory

```
TypeEvaluator<Integer> evaluator = new ArgbEvaluator();
evaluator.evaluate(0, Color.WHITE, Color.BLACK);

Animator animator = AnimatorInflater.loadAnimator(this, R.animator.animator);
animator.addListener(new Animator.AnimatorListener() {
    @Override
    public void onAnimationStart(Animator animator) { }
    @Override
    public void onAnimationEnd(Animator animator) { }
    @Override
    public void onAnimationCancel(Animator animator) { }
    @Override
    public void onAnimationRepeat(Animator animator) { }
});
animator.addPauseListener(new Animator.AnimatorPauseListener() {
    @Override
    public void onAnimationPause(Animator animator) { }
    @Override
    public void onAnimationResume(Animator animator) { }
});
animator.getDuration(); animator.setDuration(1);
animator.getStartDelay(); animator.setStartDelay(1);
animator.getTotalDuration();
animator.getInterpolator(); animator.setInterpolator(new LinearInterpolator());
animator.start(); animator.isStarted();
animator.pause(); animator.isPaused();
animator.cancel();
animator.end();
animator.resume();
animator.isRunning();

ValueAnimator valueAnimator = ValueAnimator.ofInt(1, 2, 3);
valueAnimator = ValueAnimator.ofFloat(1f, 2f, 3f);
valueAnimator = ValueAnimator.ofPropertyValuesHolder(PropertyValuesHolder.ofFloat("", 1, 2, 2));
valueAnimator.addUpdateListener(new ValueAnimator.AnimatorUpdateListener() {
    @Override
    public void onAnimationUpdate(ValueAnimator valueAnimator) { }
});
valueAnimator.getAnimatedValue();
valueAnimator.setRepeatMode(ValueAnimator.RESTART);
valueAnimator.setRepeatCount(ValueAnimator.INFINITE);

AnimatorSet animatorSet = new AnimatorSet();
animatorSet.playTogether(ValueAnimator.ofInt());
animatorSet.playSequentially(ValueAnimator.ofInt());
animatorSet.play(ValueAnimator.ofPropertyValuesHolder());


```

