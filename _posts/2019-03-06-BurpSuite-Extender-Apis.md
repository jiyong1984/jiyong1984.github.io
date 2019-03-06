---
layout: post
title: "Burp Suite Extender Apis 활용"
categories: Security_Tool
tags: burpsuite
image: http://gastonsanchez.com/images/blog/mathjax_logo.png
comments : true
---
 <B><font color="red"> 본 내용은 시스템 취약점 진단업을 하는 분들게 도움을 드리기 위해 작성된 블로그이며,
  악용시 사용한 사람의 잘못임을 인지 하길 바랍니다!</font></B>
  
  Burp sutie 툴의 Extender APIs를 사용하여 자시만의 기능을 추가 사용이 가능하다.<br>
  필자는 TobeSoft Xplatform으로 구성된 시스템을 진단할때와 body부분의 특정 구문을 추출할때 많이 사용하였다<br>
  
## Burp Suite Extender Apis 활용하기
  
### 기본지식
```
Java 문법만 알고 있으면 간단히 사용 가능하며, 여기서는 기본지식에 대해서는 다루지 않는다.
- java & eclipse
- burpsuite
```

### Extender Apis 다운로드
```
Burp Suite를 실행 후 아래 그림과 같이 [Extender]-[APIs]-[Save interface files]
버튼을 클릭하여 file를 다운로드 받는다. 저장위치는 중요하지 않다.
```
![Small Picture](\assets\img\burpsuite_apis\1.png)

```
정상적으로 다운로드되었으면 아래 그림과 같이 Interface 파일들을 확인할 수 있다.
```
![Small Picture](\assets\img\burpsuite_apis\2.png)

### Eclipse 실행 및 파일 Import
```
Eclipse 실행 후 다운로드한 Interface 파일들을 Import.(과정생략)
해당 프로젝트에 BurpExtender이라는 클래스를 하나 생성(과정생략)

Burp Suite 들어오는 HTTP 패킷을 추가 분석하는 프로그램을 작성할 예정이며
필요한 Interface(IBurpExtender, IHttpListener)를 BurpExtender.java에 Implements하여 사용한다.

```
![Small Picture](\assets\img\burpsuite_apis\3.png)

### BurpExtender.java 코드작성
```
BurpExtender.java 에 아래 코드를 추가.
processHttpMessage 메소드에서 Request, Response 데이터를 추가 분석, 수집하는 로직을 작성 할 수 있음.
```

{% highlight ruby linenos %}
package burp;
import javax.swing.SwingUtilities;
public class BurpExtender implements IBurpExtender, IHttpListener {

	private IBurpExtenderCallbacks callbacks;
	public static void main(String[] args) {
	
	}	
	
	@Override
	public void processHttpMessage(int toolFlag, boolean messageIsRequest,
			IHttpRequestResponse messageInfo) {
			
		if(messageIsRequest)
		{
			/**
			 * 이곳에 Request 메시지를 분석하는 로직을 추가할 수 있습니다.
			 */
			String s = new String(messageInfo.getRequest());
			this.callbacks.printOutput("Request Message: " +s);
		}
		else
		{
			/**
			 * 이곳에 Response 메시지를 분석하는 로직을 추가할 수 있습니다.
			 */
			String s = new String(messageInfo.getResponse());
			this.callbacks.printOutput("Response Message: " + s);
		}
	}

	@Override
	public void registerExtenderCallbacks(IBurpExtenderCallbacks callbacks) {
		
		this.callbacks = callbacks;
	    this.callbacks.setExtensionName("BurpExtender");
	    SwingUtilities.invokeLater(new Runnable()
	    {
	      public void run()
	      {
	        callbacks.registerHttpListener(BurpExtender.this);
	      }
	    });
	}
}
{% endhighlight %}

### Burp Suite에 적용하기
```
설명이 불량하지만 열심히 작성한 코드를 burpsuite에 적용하기

1. Java project를 실행가능한 .jar 파일 형태로 export(과정생략)
2. Burp Suite 실행 후 [Extender]-[Extensions]으로 이동
3. [Add]-"Extension Details"-[Select File...] 을 클릭하여 Export 한 .jar 추가
4. 하단의 [Next] 버튼을 클릭하여 마무리
```
![Small Picture](\assets\img\burpsuite_apis\4.png)


```
아래와 같이 별도 창(Load Burp Extension)이 나타나며, 우리가 코딩한 값을 출력하고 있음.
서두에도 말하였지만 Xplatform으로 만들어진 시스템은 압축된 데이터를 전송하여 평범한 방법으로는
점검하기가 어려움.

processHttpMessage 메소드에 Decompress 로직을 추가하여 분석하여야 하며 
해당 코드는 공개하지 않음.
```
![Small Picture](\assets\img\burpsuite_apis\5.png)
