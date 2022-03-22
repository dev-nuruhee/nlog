---
title: Valve란 무엇인가
published: true
---

## Valve란
Catalina 컨테이너(Engine, Host, Context)의 요청 처리 파이프라인 상에서 특정 기능을 수행하기 위해 추가될 수 있는 컴포넌트입니다.

## 특징
- Tomcat4부터 추가된 컴포넌트로 Tomcat에 들어오는 요청들에 대해 **전처리**를 수행합니다.
- Servlet Filter와 유사한 역할이나, Filter가 웹어플리케이션에 한정된 반면에 Valve는 Catalina 컨테이너 레벨에서 동작
- Tomcat에 기본으로 내장된 Valve가 다수 존재하며, Custom Valve를 개발하여 추가 가능

## 가능한 기능들
- request/response에 대한 일부 속성값 조회/변경
- request/response에 대한 wrapper 생성
- 자체적으로 response 생성 후 요청 처리 파이프라인 중단

## 주의사항
- 파이프라인 처리 흐름을 결정하는데 사용된 속성값 변경
  (예: Context에 추가된 Valve에서 request 객체의 host 속성 변경)
- 자체적으로 생성한 response를 현재 파이프라인 상의 후속 컴포넌트에 전달
- request body 접근 시 wrapper를 생성하지 않은 채로 request input stream 핸들링
- 현재 파이프라인 상에서 생성된 response에 대해 HTTP 헤더 변경
- 현재 파이프라인 상에서 생성된 response에 대해 response output stream 핸들링.


![image](https://user-images.githubusercontent.com/88364980/150447663-909c2e6d-6ed2-48c0-ada6-130729640a8f.png)
출처 : https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=gallechess&logNo=221047184041


내장 되어 있는 Valve (Tomcat 8 기준)
링크 : https://tomcat.apache.org/tomcat-8.5-doc/config/valve.html


## 사용 예시
SKB관련 사이트들에서 400에러가 떴는데, IIS나 tomcat에서 해당 오류 코드를 catch하지 못하고 tomcat 내장 페이지를 return하는 현상
내장 페이지를 return하지 않고, custom error 페이지를 return 해야함

**Custom Error page를 구성하는 로직**

``` java
import java.io.BufferedWriter;
import java.io.IOException;
import java.io.OutputStreamWriter;
import org.apache.catalina.connector.Request;
import org.apache.catalina.connector.Response;
import org.apache.catalina.valves.ErrorReportValve;

public class CustomErrorReportValve extends ErrorReportValve {
    @Override
    protected void report(Request request, Response response, Throwable t) {
        try {
            BufferedWriter out = new BufferedWriter(new OutputStreamWriter(response.getOutputStream(), "UTF8"));
            out.write("<!DOCTYPE html>");
            out.write("<html xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:th=\"http://www.thymeleaf.org\">");
            out.write("<head>");
            out.write(" <meta charset=\"utf-8\"/>");
            out.write(" <meta http-equiv=\"X-UA-Compatible\" content=\"IE=edge\"/>");
            out.write(" <meta name=\"description\" content=\"\"/>");
            out.write("</head>");
            out.write("<body>   ");
            out.write(" <script type=\"text/javascript\">");
            out.write("     alert(\"비정상적인 접근입니다.\");");
            out.write("     history.back();");
            out.write(" </script>");
            out.write("</body>");
            out.write("</html>");
            out.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

1. 위 java 파일을 jar로 만든다.
2. Tomcat lib폴더에 jar를 추가해준다.
3. tomcat의 server.xml에 설정을 추가해준다.

``` xml
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true"
errorReportValveClass="패키지명.ClassName">
<Valve className="org.apache.catalina.valves.AccessLogValve" directory="logs"
prefix="localhost_access_log" suffix=".txt" pattern="%h %l %u %t &quot;%r&quot; %s %b" />
</Host>
```

**Error Report Valve에 대한 설명**
![image](https://user-images.githubusercontent.com/88364980/150447959-cf6f6d1f-5d87-4c60-8b95-b4f88f8ae92f.png)





