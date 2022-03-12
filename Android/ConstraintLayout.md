> Thinking

```
ConstraintLayout
ConstraintLayout.LayoutParams

Guideline
Placeholder
Barrier
ConstraintSet
```

> Memory

```
androidx.constraintlayout:constraintlayout:1.1.3
androidx.constraintlayout:constraintlayout-solver:1.1.3
com.android.support.constraint:constraint-layout:
com.android.support.constraint:constraint-layout-solver:

ConstraintLayout.LayoutParams
	<location> <circle> <goneMargin>
	
	leftToLeft leftToRight # app:layout_constraintLeft_toLeftOf app:layout_constraintLeft_toRightOf
	rightToRight rightToLeft # app:layout_constraintRight_toRightOf app:layout_constraintRight_toLeftOf
	topToTop topToBottom # app:layout_constraintTop_toTopOf app:layout_constraintTop_toBottomOf
	bottomToBottom bottomToTop # app:layout_constraintBottom_toBottomOf app:layout_constraintBottom_toTopOf
	startToStart startToEnd # app:layout_constraintStart_toStartOf app:layout_constraintStart_toEndOf
	endToEnd endToStart # app:layout_constraintEnd_toEndOf app:layout_constraintEnd_toStartOf
	baselineToBaseline # app:layout_constraintBaseline_toBaselineOf
	matchConstraintPercentWidth matchConstraintPercentHeight # app:layout_constraintWidth_percent app:layout_constraintHeight_percent
	matchConstraintMaxWidth matchConstraintMaxHeight # app:layout_constraintWidth_max app:layout_constraintHeight_max
	matchConstraintMinWidth matchConstraintMinHeight # app:layout_constraintWidth_min app:layout_constraintHeight_min
	horizontalBias verticalBias # app:layout_constraintHorizontal_bias app:layout_constraintVertical_bias
	circleAngle # app:layout_constraintCircleAngle
	circleConstraint # app:layout_constraintCircle
	circleRadius # app:layout_constraintCircleRadius
	constrainedWidth constrainedHeight # app:layout_constrainedWidth app:layout_constrainedHeight
	goneLeftMargin goneRightMargin # app:layout_goneMarginLeft app:layout_goneMarginRight
	goneTopMargin goneBottomMargin # app:layout_goneMarginTop app:layout_goneMarginBottom
	goneStartMargin goneEndMargin # app:layout_goneMarginStart app:layout_goneMarginEnd
	guideBegin guideEnd # app:layout_constraintGuide_begin app:layout_constraintGuide_end
	guidePercent # app:layout_constraintGuide_percent
	horizontalWeight verticalWeight # app:layout_constraintHorizontal_weight app:layout_constraintVertical_weight
	horizontalChainStyle verticalChainStyle # app:layout_constraintHorizontal_chainStyle app:layout_constraintVertical_chainStyle spread
	dimensionRatio # app:layout_constraintDimensionRatio 1:1
	matchConstraintDefaultWidth matchConstraintDefaultHeight # app:layout_constraintHeight_default app:layout_constraintWidth_default spread
	# app:layout_constraintLeft_creator app:layout_constraintRight_creator app:layout_constraintTop_creator app:layout_constraintBottom_creator
	# app:layout_constraintBaseline_creator
	# app:constraint_referenced_ids
	# app:constraintSet

```

