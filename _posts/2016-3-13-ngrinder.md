---
layout: post
title: nGrinder�� �Ẹ��
cover: cover.jpg
---


# nGrinder 


## ����

nGrinder�� ���̹����� 2011����� �����ϰ� �ִ� ���¼ҽ� ���� ���� �����Դϴ�. 

�� ���񽺸� �����ϸ鼭 ������ ������ ���ɿ� ���ؼ� ������ ��� ������ �ŷ� �����մϴ�. 

(�̹��� Ư���� ��ȸ�� �������� write-back�� �����ϸ鼭 ���� ��ȸ�� ���� Ʈ������� ���� ��� ��ȸ���� ���ϴ� ��Ĵ�� write-back�� �����ϴ��� �׽�Ʈ �ϰ� ������ �е鵵 ��� ���Դϴ�.)

�׷��� �׽�Ʈ�� �ϸ鼭 ��Ģ�� �԰��� ��Ȯ�� ��ġ �ڷḦ ��� �ʹٸ� ���� ���� ������ ����ϴ� ���� �ʿ����Դϴ�.

���� �׽�Ʈ���ϸ� �ε� �׽�Ʈ�� ��Ʈ���� �׽�Ʈ �� ���� ���鿡 �׽�Ʈ�� ���� �� �ֽ��ϴ�.

nGrinder�� �̷��� ���� �׽�Ʈ�� �����ϰ� Ȥ�� ��ũ��Ʈ�� �ۼ��Ͽ� ������ �׽�Ʈ���� Ŀ���� �� �ֵ��� �����մϴ�. 



## ���� ���

ngrinder�� ���¼ҽ��� �����Ǿ� �ֱ� ������ 

https://sourceforge.net/projects/ngrinder/files/ ���� ���� �ٿ� ������ ���� �ֽ��ϴ�. 

��ġ ������� ���ÿ��� ���� �����ϰų� ���� ȯ�濡�� ������ ���� �ְ� ����� �پ��մϴ�. (�Ʒ� �ϴ� ��ũ�� �����Ͻø� �˴ϴ�.)

�ٸ� �ᱹ �׽�Ʈ�� �����ϱ� ���� ���ҽ��� ���ÿ��� �����ϴ� �ͱ��� ����������,
��ġ �� ���ÿ��� ��� ���� �ڽ�Ʈ�� ��� ���񽺰� ���� ���� ���������� �����ϴ� ���� �׽�Ʈ�� ���� ȯ���� �������� �鿡�� �浹�ǹǷ� �����մϴ�. 

> **���� �系������ ngrinder�� ���� �׽�Ʈ�� �� �ִ� ȯ���� �����ϰ� �ֽ��ϴ�.  
>  ����� URL
 
 ---
### ���� ȭ��
 
 �α����� �ϸ鼭 ���� ���� ȭ���� ���� �� �ֽ��ϴ�. 
 �����ϰ� �׽�Ʈ�� �� �� �ֵ��� Quick Start �޴��� �ִµ� �̰��� ���ϴ� ������ URL�� �Է��մϴ�. 
 �׽�Ʈ�� �����ϱ� ���� ��ũ��Ʈ �� ������ �� �ִµ� groovy�� jython, groovy maven project �߿� ������ �� �ֽ��ϴ�.

---
### ���� ������


������Ʈ�� ���� ������Ʈ�� �������� ���� �����ϰ�
������ **�ڡ�IDC**�� �����մϴ�.

�׽�Ʈ �Ⱓ�� �ɼ����� �����ϸ� �ش� �ð����� �׽�Ʈ�� ��� �����ϰ�
Ƚ���� ������ ��� �� Ƚ����ŭ �����մϴ�. 
(���� ������ ��쿡�� ������ ���� ���� �� �� �ֽ��ϴ�.)

�� �� �پ��� �ɼ��̳� ������ �׽�Ʈ�� Ŀ���͸���¡ �ϱ� ���ؼ��� ��ũ��Ʈ�� �����ؾ��մϴ�.

��ũ��Ʈ���� R HEAD�� Ŭ���ϸ� �׷��ũ��Ʈ �ڵ� ������ ���� �� �ֽ��ϴ�.
(���ο��� �����ߴ� ��ũ��Ʈ ������� �����˴ϴ�.)

---
### ��ũ��Ʈ


������ �� ���ø� ��ġä�� �е鵵 �����ð����� ���� �������� �ۼ��߾��� TC�� ���������� �����ϴ�. 

```
@RunWith(GrinderRunner)
class TestRunner {

	public static GTest test
	public static HTTPRequest request
	public static NVPair[] headers = []
	public static NVPair[] params = []
	public static Cookie[] cookies = []

	@BeforeProcess
	public static void beforeProcess() {
		HTTPPluginControl.getConnectionDefaults().timeout = 6000
		test = new GTest(1, "alpha-happynews.nhnent.com")
		request = new HTTPRequest()
		grinder.logger.info("before process.");
	}

	@BeforeThread 
	public void beforeThread() {
		test.record(this, "test")
		grinder.statistics.delayReports=true;
		grinder.logger.info("before thread.");
	}
	
	@Before
	public void before() {
		request.setHeaders(headers)
		cookies.each { CookieModule.addCookie(it, HTTPPluginControl.getThreadHTTPClientContext()) }
		grinder.logger.info("before thread. init headers and cookies");
	}

	@Test
	public void test(){
		HTTPResponse result = request.GET("http://alpha-happynews.nhnent.com", params)

		if (result.statusCode == 301 || result.statusCode == 302) {
			grinder.logger.warn("Warning. The response may not be correct. The response code was {}.", result.statusCode); 
		} else {
			assertThat(result.statusCode, is(200));
		}
	}
}
```
������Ʈ�� �żҵ� ��ĺ���, ����� ���̳� ��Ű���� �׽�Ʈ�� ���ϴ� ������ �Է��Ͽ� �׽�Ʈ�� ���� ������� ������ �� �ֽ��ϴ�. 
���� �α����� �ʿ��ϰų� Ư�� ������ �ʿ��� �������� ���ҽ��� �ʿ��� ��쿡�� ���� ������ �� �� �ֽ��ϴ�. 

��ũ��Ʈ�� ��� �ۼ��� �� '��ũ��Ʈ ����'�� ���� �׽�Ʈ�� ����� ���ư����� Ȯ���մϴ�.

�׽�Ʈ�� ���� �׽�Ʈ �ڵ尡 Ȯ���� �Ϸ�Ǿ����� '���� �� ����'�� ���� �׽�Ʈ�� ���� �� �� �ֽ��ϴ�. 

---
### ���� ȭ�� 


�׽�Ʈ�� �Ϸ�Ǹ� ���� ���� ���� ����� ���� �� �ֽ��ϴ�. �׽�Ʈ ������ �پ��ϰ� �Ѵٸ� �� ��ġ �ִ� �׽�Ʈ�� �Ͻ� �� �ֽ��ϴ�.
 

---

` ���������� �̷��� ���� ���� ��ü�� DDoS ���ݰ� �ǹ̻����� �����Ƿ� �ʿ� �̻��� ���� ���� ��Ʈ���� �׽�Ʈ�� �����Ͻô� ���� �����ϼž� �� �� �����ϴ�. �Ф� `


---
### ���� ����Ʈ 

* http://naver.github.io/ngrinder/
* http://deview.kr/2013/detail.nhn?topicSeq=2
* http://junoyoon.tistory.com/entry/nGrinder-33-%EC%84%A4%EC%B9%98%EB%B0%A9%EB%B2%95
* http://www.groovy-lang.org/