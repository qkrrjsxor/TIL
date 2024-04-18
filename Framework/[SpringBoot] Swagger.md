# Swagger
Swagger는 대규모로 API를 설계하고 문서화 하는데 도움을 주는 오픈소스 API 문서화 프레임워크입니다. 이는 API를 시각적으로 표현하고, API를 통해 어떤 종류의 액션이 가능한지 보여주며, 실제로 해당 API를 테스트 해 볼 수 있게 해줍니다.

## Swagger의 특징
1. 시각적 표현 : API를 직관적으로 이해할 수 있도록 Swagger UI를 지원하여 시각적으로 API를 표현하는 기능을 제공합니다. 이를 통해 API의 구조와 작동 방식을 쉽게 파악할 수 있습니다.
2. 실시간 테스트 : API를 실시간으로 테스트하고 디버깅하는 기능을 제공합니다. 이를 통해 API의 정확성을 확인할 수 있으며 더 빠르게 문제를 찾아낼 수 있습니다.
3. 문서 자동화 : API 문서를 자동으로 생성하고 업데이트하는 기능을 제공합니다. 이를 통해 수동으로 문서를 업데이트하는 수고를 줄이고, API문서 최신 정보를 확인할 수 있으므로 효율적 입니다.

## Swagger 설정 방법
SpringBoot에 Swagger 사용하는 방법
1. 의존성 추가(Maven)
    먼저 pom.xml 파일에 Swagger(springdoc) 의존성을 추가합니다. 이를 통해 Swagger 라이브러리를 사용할 수 있게 됩니다.
```xml
		<dependency>
		    <groupId>org.springdoc</groupId>
		    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
		    <version>2.4.0</version>
		</dependency>
```
2. Configuration 설정
    Swagger UI 문서의 기본 설명을 부여하기 위해 다음 예시와 같이 Configuration을 설정 합니다.
```java
@Configuration // 스프링 설정 클래스임을 나타냅니다.
public class SwaggerConfig {
    @Bean // 스프링 빈으로 등록합니다.
    public OpenAPI openAPI() {
        return new OpenAPI()
                .components(new Components()) // API 구성 요소를 설정합니다.
                .info(apiInfo()); // API 정보를 설정합니다.
    }

    private Info apiInfo() {
        return new Info()
                .title("문서 API") // API 제목을 설정합니다.
                .description("<h3>RestAPI 문서 내용을 다음과 같이 제공합니다.</h3>") // API 설명을 설정합니다.
                .version("1.0.0"); // API 버전을 설정합니다.
    }
}
```

3. Swagger 기본 설정으로 여러 속성들을 application에 지정할 수 있습니다.
```
# 패키지를 스캔하여 API 문서를 생성
springdoc.packages-to-scan=*

# API의 기본 들어오는 meida type을 설정합니다
springdoc.default-consumes-media-type=application/json;charset=UTF-8

# API의 기본 반환하는 meida type을 설정합니다
springdoc.default-produces-media-type=application/json;charset=UTF-8

# Swagger UI 접속 경로 설정
springdoc.swagger-ui.path=/swagger-ui.html

# Swagger 기본 테스트용 Petstore URL 비활성화(기본값 : false)
springdoc.swagger-ui.disable-swagger-default-url=true

# 요청 처리 시간을 밀리세컨드 단위로 표시(기본값 : false)
springdoc.swagger-ui.display-request-duration=true

# Swagger UI에서 메소드명 기준으로 알파벳 순 정렬
springdoc.swagger-ui.operations-sorter=alpha

```

4. Swagger 문서화 어노테이션 활용
    Springdoc에서는 API를 문서화 할 때 다양한 어노테이션을 사용합니다. 주요 어노테이션은 다음과 같습니다.
    - @Tag : API를 그룹화 하거나 분류하는데 사용. API를 특정 카테고리나 그룹에 할당
    - @Operation : 개별 API 작업에 대한 정보 제공. API 작업의 요약, 설명, 태그 등 표시
    - @Parameter : API 작업의 매개변수에 대한 정보 제공. 매개변수의 이름, 설명 ,필수 여부 등
  
## API 테스트 방법
1. API 섹션을 클릭하여 확장하면 API의 설명, 요청 파라미터, 응답 형식 등을 확인 할 수 있습니다.
2. Try it out 버튼을 클릭하여 API 직접 테스트. 요청 파라미터를 입력할 수 있는 필드가 활성화 됩니다.
3. 요청 파라미터를 입력하고 Execute 버튼 클릭을 하면 결과가 하단에 표시됩니다. 응답 코드, 응답 헤더, 응답 본문 등 확인 가능