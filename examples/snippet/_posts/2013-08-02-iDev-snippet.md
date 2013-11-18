---
layout: nil
title: iDev snippet
---


>	#pragma mark -
	#pragma mark Encode Chinese to ISO8859-1 in string
	-(NSString *)encode2UTF8Str:(NSString *)encodeStr {
	//  URL

	//    CFStringRef nonAlphaNumValidChars = CFSTR("![        DISCUZ_CODE_1        ]’()*+,-./:;=?@_~");

	//    NSString *preprocessedString = (__bridge NSString *)CFURLCreateStringByReplacingPercentEscapesUsingEncoding(kCFAllocatorDefault, (CFStringRef)encodeStr, CFSTR(""), kCFStringEncodingUTF8);

	//    NSString *newStr = (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(kCFAllocatorDefault,(CFStringRef)preprocessedString,NULL,nonAlphaNumValidChars,kCFStringEncodingUTF8);
    
		CFString    
    	NSStringEncoding enc = CFStringConvertEncodingToNSStringEncoding(kCFStringEncodingGB_18030_2000);

    	NSString *newStr = [[NSString alloc] initWithBytes:(__bridge const void *)(encodeStr) length:[encodeStr length] encoding:enc];

    	return newStr;
	}

	#pragma mark -
	#pragma mark Encode Chinese to GB2312 in URL
	-(NSString *)encode2GB2312Str:(NSString *)encodeStr {
   		CFStringRef nonAlphaNumValidChars = CFSTR("![        DISCUZ_CODE_1        ]’()*+,-./:;=?@_~");

    	NSString *preprocessedString = (__bridge NSString *)CFURLCreateStringByReplacingPercentEscapesUsingEncoding(kCFAllocatorDefault, (CFStringRef)encodeStr, CFSTR(""), kCFStringEncodingGB_18030_2000);

    	NSString *newStr = (__bridge NSString *)CFURLCreateStringByAddingPercentEscapes(kCFAllocatorDefault,(CFStringRef)preprocessedString,NULL,nonAlphaNumValidChars,kCFStringEncodingGB_18030_2000);

    	return newStr;
	}