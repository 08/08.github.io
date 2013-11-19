---
layout: nil
title: iOS 6/7 UISearchBar Background color
---

#### 清除搜索框背景色

> 
	//for iOS6
	for (UIView *subview in self.search.subviews) {
    	if ([subview isKindOfClass:NSClassFromString(@"UISearchBarBackground")]) {
        	[subview removeFromSuperview];
        	break;
   	 }  
	}

>
	//for iOS 7 
	if ([self.search respondsToSelector:@selector(barTintColor)]) {
		[self.search setBarTintColor:[UIColor clearColor]];
	}
