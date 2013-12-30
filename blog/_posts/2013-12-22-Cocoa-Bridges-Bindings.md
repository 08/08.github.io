---
layout: post
title: Cocoa Bridges&amp;Bindings
author: Ethan
---

#### HTML5 vs. native vs. hybrid mobile apps

#### hybrid mobile apps -- iOS
开发一个混合应用的App底层支持模块, 需要提供适合自己需要的Bridge支持,熟悉特定平台的编译器支持，就iOS来说，你就得对苹果的ARMv7Assembler和Apple-GCC-LLVM熟悉
，然后才是对特定平台提供的原生应用开发框架的支持 

下面是一个对于iOS开发混合应用的Bridge支持的头文件    

>
			    
	#import "AppCoreProxy.h"
    
    @class AppCoreHost;
    
    @interface Bridge : NSObject {
    @private
    	id callback;
    	NSString *basename;
    @protected
    	NSURL *url;
    	AppCoreHost *host;
    }
    
    -(id)initWithHost:(TiHost*)host;
    
    -(void)boot:(id)callback url:(NSURL*)url preload:(NSDictionary*)preload;
    
    -(void)booted;
    
    -(void)shutdown:(NSCondition*)condition;
    
    -(void)gc;
    
    -(AppCoreHost*)host;
    
    - (NSString*)basename;
    
    @end
    