---
layout: post
title: 实现和Roambi里面的图表的类似效果-可旋转的PieChart
author: Ethan
---

要定义
	仿射变换矩阵CGAffineTransform startTransform  
    旋转的轴心CGPoint wheelCenter  
    自动跳回饼图对应块的中部的方法- (float) midOfTouchendClove: (float)ang  

>  添加基本的Frame

	- (void)setFrame:(CGRect)frame {
	    [super setFrame:frame];
    
 	   fontSize = frame.size.width / 20;
	    if (fontSize < 9) fontSize = 9;
    
	    // 半径和圆心
	    centerX = frame.size.width/2 ;
	    centerY = frame.size.height/2;
	    radius = centerX < centerY ? centerX : centerY;
	    radius *= kRadiusPortion;
	    [self setNeedsDisplay];
	}

>  添加饼块

		- (void)addSlicePortion:(float)slicePortion withName:(NSString *)name {
			[sliceNames addObject:(name ? name : @"")];
		    [slicePortions addObject:nFloat(slicePortion)];
			float sumSoFar = [self pointAtIndex:-1];
			[slicePointsIn01 addObject:nFloat(sumSoFar + slicePortion)];
			[self addLabelForLastName];
		}

>  绘制背景图层， 注意饼图主要由三个图层组成

	- (void)drawRect:(CGRect)rect {
		if ([slicePortions count] == 0) {
			NSLog(@"%s -- called with no slicePortions data", __FUNCTION__);
			return;
		}
	    
		// 绘制白色背景
		// 遮盖alpha值小于1的调色组件
		CGContextRef context = UIGraphicsGetCurrentContext();
		CGContextBeginPath(context);
		CGContextAddArc(context, centerX, centerY, radius, 0, 2*M_PI, 1);
		CGContextSetRGBFillColor(context, 1.0, 1.0, 1.0, 1.0);
		CGContextFillPath(context);
	    
	    CGContextSaveGState(context);
	//    float shadowSize = radius / 15.0;
	//	CGContextSetShadow(context, CGSizeMake(shadowSize, shadowSize), shadowSize);
	    CGContextBeginTransparencyLayer(context, NULL);
	    for (int i = 0; i < [slicePortions count]; ++i) {
	        [self drawSlice:i inContext:context];
	    }
	    CGContextEndTransparencyLayer(context);
	    CGContextRestoreGState(context);
		/*
	     // Draw the glare.
		CGContextBeginPath(context);
		CGContextAddArc(context, centerX, centerY, radius, 0, 2*M_PI, 1);
		CGContextClip(context);
		CGContextBeginPath(context);
		CGContextAddArc(context, centerX - radius * 0.5, centerY - radius * 0.5,
						radius * 1.1, 0, 2*M_PI, 1);
		CGContextClip(context);
		
		// Set up the gradient for the glare.
		size_t num_locations = 2;
		CGFloat locations[2] = {0.0, 1.0};
		CGFloat components[8] = {1.0, 1.0, 1.0, 0.0, 1.0, 1.0, 1.0, 0.45};
		CGGradientRef gradient = CGGradientCreateWithColorComponents(colorspace, components,
																	 locations, num_locations);
		CGContextDrawLinearGradient(context, gradient,
									CGPointMake(centerX + radius * 0.6, centerY + radius * 0.6),
									CGPointMake(centerX - radius, centerY - radius), 0);
		CGGradientRelease(gradient);
	     */
	}

>  绘制饼块

	- (void)drawSlice:(int)index inContext:(CGContextRef)context {
	    
		CGFloat startAngle = 2 * M_PI * [self pointAtIndex:index];
		CGFloat endAngle = 2 * M_PI * [self pointAtIndex:(index + 1)];
		
		CGMutablePathRef path = CGPathCreateMutable();
		CGPathAddArc(path, NULL, centerX, centerY, radius, startAngle, endAngle, 0);
		CGPathAddLineToPoint(path, NULL, centerX, centerY);
		CGPathCloseSubpath(path);
		
		// Draw the shadowed slice.
		CGContextSaveGState(context);
		CGContextAddPath(context, path);
		CGFloat red, green, blue;
		[self getRGBForIndex:index red:&red green:&green blue:&blue];
		CGContextSetRGBFillColor(context, red, green, blue, 0.35);
		CGContextFillPath(context);
		CGContextRestoreGState(context);
	    ////	
		// Draw the left-right gradient.
		CGContextSaveGState(context);
		CGContextAddPath(context, path);
		CGContextClip(context);
		CGGradientRef gradient = [self newGradientForIndex:index];
		CGContextDrawLinearGradient(context, gradient,
	                                CGPointMake(centerX + radius, centerY),
	                                CGPointMake(centerX - radius, centerY), 0);
		CGGradientRelease(gradient);
		CGContextRestoreGState(context);
	    //	
		// Draw the slice outline.
		CGContextSaveGState(context);
		CGContextAddPath(context, path);
		CGContextClip(context);
		CGContextAddPath(context, path);
		CGContextSetLineWidth(context, 0.5);
		UIColor* darken = [UIColor colorWithWhite:0.0 alpha:0.2];
		CGContextSetStrokeColorWithColor(context, darken.CGColor);
		CGContextStrokePath(context);
		CGContextRestoreGState(context);
		
		CGPathRelease(path);
	}

>  // 添加比例，标签，饼块颜色，罗盘饼图轴长

	- (CGGradientRef)newGradientForIndex:(int)index;
	- (void)addLabelForLastName;
	- (void)getRGBForIndex:(int)index red:(float *)red green:(float *)green blue:(float *)blue;
	- (float)dist(float x1, float y1, float x2, float y2);
	- (float)approxDistFromCenter:(CGRect)rect;
