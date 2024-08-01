
# 리팩토링 설명 수업

## 1장 서론

### 1.1 수업 목표 소개
리팩토링의 개념과 중요성을 이해하고, 코드 품질을 향상시키기 위한 리팩토링 기법을 습득하는 것을 목표로 합니다.

### 1.2 리팩토링의 정의 및 중요성 설명
리팩토링은 코드의 기능을 변경하지 않고, 코드의 구조를 개선하는 작업입니다. 이를 통해 코드의 가독성, 유지보수성, 확장성을 높일 수 있습니다.

## 2장 리팩토링의 기본 개념

### 2.1 리팩토링의 정의
리팩토링은 기존 코드를 보다 이해하기 쉽고 수정하기 쉽게 만드는 일련의 과정입니다.

### 2.2 코드 스멜(Code Smell)이란?
코드 스멜은 코드에서 악취가 나는 부분으로, 리팩토링이 필요한 지점을 의미합니다. 이는 복잡하고 이해하기 어려운 코드를 나타냅니다.

### 2.3 리팩토링의 장점 및 필요성
- **가독성 향상:** 코드를 읽기 쉽게 만들어 협업을 원활하게 합니다.
- **유지보수 용이:** 코드를 쉽게 수정하고 확장할 수 있습니다.
- **버그 감소:** 코드 구조를 개선하면서 잠재적인 버그를 발견하고 수정할 수 있습니다.

## 3장 리팩토링의 원칙과 규칙

### 3.1 리팩토링 원칙
- **작게 자주 리팩토링:** 작은 단위로 자주 리팩토링하여 큰 변화를 피합니다.
- **테스트 주도:** 리팩토링 전후에 코드가 정상적으로 동작하는지 확인합니다.

### 3.2 리팩토링 시 주의할 점
- 기능을 변경하지 않습니다.
- 리팩토링 전후에 테스트를 통해 코드가 동일하게 동작하는지 확인합니다.

### 3.3 Clean Code에서 제시하는 리팩토링 규칙
- **의도를 분명히:** 함수와 변수의 이름을 명확하게 작성합니다.
- **중복 제거:** 중복된 코드를 제거합니다.
- **작은 함수:** 한 가지 일만 하는 작은 함수로 분리합니다.

## 4장 리팩토링의 종류 및 기법

### 4.1 메소드 추출 (Extract Method)

#### 예제: 자바
```java
public class Order {
    private List<Item> items;

    public double calculateTotalPrice() {
        double totalPrice = 0;
        for (Item item : items) {
            double itemPrice = item.getPrice() * item.getQuantity();
            double discount = itemPrice * item.getDiscount();
            double finalPrice = itemPrice - discount;
            totalPrice += finalPrice;
        }
        return totalPrice;
    }
}
```

#### 리팩토링 후
```java
public class Order {
    private List<Item> items;

    public double calculateTotalPrice() {
        double totalPrice = 0;
        for (Item item : items) {
            totalPrice += calculateItemPrice(item);
        }
        return totalPrice;
    }

    private double calculateItemPrice(Item item) {
        double itemPrice = item.getPrice() * item.getQuantity();
        double discount = itemPrice * item.getDiscount();
        return itemPrice - discount;
    }
}
```

### 4.2 변수 추출 (Extract Variable)

#### 예제: 자바스크립트
```javascript
function getUserInfo(user) {
    return `Name: ${user.firstName} ${user.lastName}, Age: ${user.age}, Email: ${user.email}`;
}
```

#### 리팩토링 후
```javascript
function getUserInfo(user) {
    const fullName = \`\${user.firstName} \${user.lastName}\`;
    return `Name: ${fullName}, Age: ${user.age}, Email: ${user.email}`;
}
```

### 4.3 클래스 추출 (Extract Class)

#### 예제: 자바
```java
public class Person {
    private String name;
    private String address;
    private String phoneNumber;
    private String email;
}
```

#### 리팩토링 후
```java
public class Person {
    private String name;
    private ContactInfo contactInfo;
}

public class ContactInfo {
    private String address;
    private String phoneNumber;
    private String email;
}
```

## 5장 리팩토링 도구 소개

### 5.1 IDE 내장 리팩토링 도구
- 대부분의 현대 IDE는 리팩토링 도구를 내장하고 있어 손쉽게 리팩토링을 수행할 수 있습니다.

### 5.2 전용 리팩토링 툴
- 더 복잡한 리팩토링 작업을 위해 전용 툴을 사용할 수 있습니다.

## 6장 리팩토링 실습

### 6.1 간단한 예제 코드 제공
- 실습을 위해 간단한 예제 코드를 제공합니다.

### 6.2 코드 스멜 찾기
- 예제 코드에서 코드 스멜을 찾습니다.

### 6.3 리팩토링 적용 및 결과 확인
- 리팩토링을 적용한 후, 결과를 비교하여 개선된 부분을 확인합니다.

## 7장 리팩토링의 사례 연구

### 7.1 성공적인 리팩토링 사례
- 성공적으로 리팩토링된 사례를 소개합니다.

### 7.2 실패 사례 및 교훈
- 리팩토링이 실패한 사례와 그로부터 얻은 교훈을 공유합니다.

## 8장 결론 및 Q&A

### 8.1 주요 내용 요약
- 오늘 수업에서 다룬 주요 내용을 요약합니다.

### 8.2 질문과 답변 시간
- 참석자들의 질문을 받고 답변하는 시간을 가집니다.

### 8.3 추가 학습 자료 소개 (책, 온라인 리소스 등)
- 추가로 학습할 수 있는 자료들을 소개합니다.
  - [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
  - [Refactoring](https://martinfowler.com/books/refactoring.html)


## 9장 개인적인 견해

### 9.1 if-else 문에 대한 견해

### 9.2 함수, 변수 명 짓기의 중요성 및 방법
좋은 함수와 변수 이름은 코드의 가독성과 이해도를 크게 향상시킵니다. 이름을 짓는 데 있어 다음과 같은 원칙을 따르는 것이 좋습니다:
- **의도를 분명히:** 함수나 변수가 하는 일을 명확하게 설명하는 이름을 사용합니다.
- **일관성 유지:** 프로젝트 전체에서 일관된 명명 규칙을 따릅니다.
- **축약어 지양:** 축약어보다는 전체 단어를 사용하여 의미를 명확히 합니다.
- **문맥 제공:** 함수나 변수가 속한 클래스나 모듈의 문맥을 반영하는 이름을 사용합니다.

예시:
- 나쁜 예: `calc` (무엇을 계산하는지 불명확)
- 좋은 예: `calculateTotalPrice` (총 가격을 계산하는 함수임을 명확히 함)

#### 함수명 예시

##### 나쁜 예:
- `calc` (무엇을 계산하는지 불명확)
- `doStuff` (구체적인 동작을 알 수 없음)
- `handle` (어떤 것을 처리하는지 모호함)

##### 좋은 예:
- `calculateTotalPrice` (총 가격을 계산하는 함수임을 명확히 함)
- `fetchUserData` (사용자 데이터를 가져오는 함수)
- `processOrder` (주문을 처리하는 함수)

#### 명명 규칙

##### 함수:
함수 이름은 일반적으로 동사+명사 형태로 작성합니다.
- 예시: `getUserInfo`, `sendEmailNotification`, `updateOrderStatus`

##### 상수:
상수 이름은 모든 글자를 대문자로 하고, 단어 사이에 언더스코어를 사용합니다.
- 예시: `MAX_RETRY_ATTEMPTS`, `DEFAULT_TIMEOUT`, `PI`

##### 변수:
변수 이름은 일반적으로 소문자로 시작하며, camelCase를 사용합니다.
- 예시: `userName`, `orderCount`, `isVerified`

### 9.5 주석에 관해
주석은 코드의 의도를 설명하고, 다른 개발자가 코드를 이해하는 데 도움을 줍니다. 그러나 지나치게 많은 주석은 코드의 가독성을 떨어뜨릴 수 있습니다. 주석 작성 시 다음 원칙을 따르는 것이 좋습니다:
- **필요한 곳에만:** 코드 자체로 충분히 설명되지 않는 부분에만 주석을 추가합니다.
- **명확하고 간결하게:** 불필요한 설명을 피하고, 간결하게 작성합니다.
- **코드 변경 시 업데이트:** 코드가 변경되면 주석도 함께 업데이트하여 일관성을 유지합니다.

예시:
- 나쁜 예: `// 변수 선언` (너무 일반적이고 불필요한 주석)
- 좋은 예: `// 고객의 총 구매 금액을 계산하는 함수` (의도를 명확히 설명)

주석은 코드의 명확성과 유지보수성을 높이는 도구로 사용되어야 하며, 코드 자체가 가능한 한 명확하게 작성되는 것이 가장 중요합니다.




## 10장 리팩토링 예제

### 리팩토링 전 코드

```java
public class OrderProcessor {
    public void process(Order order) {
        if (order != null) {
            if (order.getItems() != null && !order.getItems().isEmpty()) {
                double totalPrice = 0;
                for (Item item : order.getItems()) {
                    double itemPrice = item.getPrice() * item.getQuantity();
                    double discount = 0;
                    if (item.getDiscount() > 0) {
                        discount = itemPrice * item.getDiscount();
                    }
                    double finalPrice = itemPrice - discount;
                    totalPrice += finalPrice;
                }
                if (order.getCustomer() != null) {
                    Customer customer = order.getCustomer();
                    if (customer.getAddress() != null) {
                        Address address = customer.getAddress();
                        if (address.getCity() != null) {
                            String city = address.getCity();
                            if (city.equals("New York")) {
                                totalPrice += 10;
                            }
                        }
                    }
                }
                order.setTotalPrice(totalPrice);
                order.setProcessed(true);
                if (order.isExpress()) {
                    System.out.println("Order processed with express delivery");
                } else {
                    System.out.println("Order processed with standard delivery");
                }
            } else {
                System.out.println("Order has no items");
            }
        } else {
            System.out.println("Order is null");
        }
    }
}
```

### 리팩토링 후 코드
```java
public class OrderProcessor {
    
    public void process(Order order) {
        if (order == null) {
            System.out.println("Order is null");
            return;
        }
        
        if (!hasItems(order)) {
            System.out.println("Order has no items");
            return;
        }
        
        double totalPrice = calculateTotalPrice(order);
        totalPrice = applyLocationSurcharge(totalPrice, order.getCustomer());
        
        order.setTotalPrice(totalPrice);
        order.setProcessed(true);
        
        printDeliveryMethod(order.isExpress());
    }

    private boolean hasItems(Order order) {
        return order.getItems() != null && !order.getItems().isEmpty();
    }

    private double calculateTotalPrice(Order order) {
        double totalPrice = 0;
        for (Item item : order.getItems()) {
            totalPrice += calculateItemPrice(item);
        }
        return totalPrice;
    }

    private double calculateItemPrice(Item item) {
        double itemPrice = item.getPrice() * item.getQuantity();
        double discount = (item.getDiscount() > 0) ? itemPrice * item.getDiscount() : 0;
        return itemPrice - discount;
    }

    private double applyLocationSurcharge(double totalPrice, Customer customer) {
        if (customer != null && customer.getAddress() != null && "New York".equals(customer.getAddress().getCity())) {
            totalPrice += 10;
        }
        return totalPrice;
    }

    private void printDeliveryMethod(boolean isExpress) {
        if (isExpress) {
            System.out.println("Order processed with express delivery");
        } else {
            System.out.println("Order processed with standard delivery");
        }
    }
}

```