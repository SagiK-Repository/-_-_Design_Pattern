문서정보 : 2023.10.20. 작성, 작성자 [@SAgiKPJH](https://github.com/SAgiKPJH)

<br>

# Design Pattern

- 디자인 패턴
  - 디자인 패턴은 소프트웨어 개발에서 반복적으로 발생하는 문제를 효율적으로 해결하기 위한 재사용 가능한 해결책을 의미한다.
  - 코드의 재사용성, 모듈성, 유지 보수성을 높이는데 도움이 된다.
- 대표적인 패턴으로는 다음 3가지가 있다.
  - 생성 패턴 : 객체가 생성되는 방식을 중점
  - 구조 패턴 : 클래스와 객체를 더 큰 구조로 구성
  - 행위 패턴 : 객체 간의 상호작용과 책임 분배에 초점

<br>

### 목차

- [ ] 객체지향 5원칙 (SOLID 원칙)
- [ ] 0. 간단 노트
- [ ] 1. 생성 패턴
  - [ ] 
- [ ] 2. 구조 패턴
- [ ] 3. 행위 패턴

<br>

### 제작자
[@SAgiKPJH](https://github.com/SAgiKPJH)


<br>

---

# 객체지향 5원칙 (SOLID 원칙)

- SRP (Single Responsibility Principle)
  - 단일 책임 원칙
  - 객체는 오직 하나의 책임(하나의 변경의 이유만)을 가져야 한다.
  - 사칙연산 함수를 가지고 있는 계산 클래스가 있다고 치자. 이 상태의 계산 클래스는 오직 사칙연산 기능만을 책임진다.
  - 단일 책임 원칙은 클래스의 목적을 명확히 함으로써 구조가 난잡해지거나 수정 사항이 불필요하게 넓게 퍼지는 것을 예방하고 기능을 명확히 분리.
- OCP (Open-Closed Principle)
  - 개방-폐쇄 원칙
  - 확장에 대해 열려 있어야 하고, 수정에 대해서는 닫혀 있어야 한다.
  - 확장 : IShape -> Cirecle, Rectangle, 갈아끼울 수 있게 구성
  - 수정 : AreCalculator에서는 IShape에 또 다른 내용이 추가 되어도 수정 필요 없도록 구성
  - `갈아끼울거 추가해도 다른거 수정 없도록 구성`
- LSP (Liskov Substitution Principle)
  - 리스코프 치환 원칙
  - 자식 클래스는 언제나 자신의 부모 클래스를 대체할 수 있다.
  - 부모 자리에 자식클래스를 넣어도 잘 작동해야 한다.
- ISP (Interface Segregation Principle)
  - 인터페이스 분리 원칙
  - 클라이언트에서 사용하지 않는 메서드는 사용해선 안 된다. 
  - 클라이언트가 자신이 사용하지 않는 메서드에 의존하도록 강요받지 않아야 한다는 원칙.
  - 인터페이스를 다시 작게 나누어 만든다.
  - 인터페이스의 SRP
- DIP (Dependency Inversion Principle)
  - 의존성 역전의 원칙
  - 갈아끼울 수 있어야 한다.

<br><br>


<br><br>

# 1. 생성 패턴

### 팩토리 패턴 (Factory Method)

- 객체를 생성하도록 하는 디자인 패턴
- 객체 생성 로직을 서브 클래스에게 위임
- 사용자가 직접 클래스 X, 팩토리 메서드를 통해 객체를 생성하도록 하는 디자인 패턴
- Example
  - 클라이언트 코드에서 직접 개나 고양이 객체를 생성하지 않고, 팩토리 메서드로 원하는 동물 객체를 얻을 수 있습니다.
```cs
Dog youDog = newDog(); // 직접 생성 X하도록 합니다.

IAnimal myDog = AnimalFactory.CreateAnimal("Dog");
myDog.Speak();  // Outputs: Bark!

IAnimal myCat = AnimalFactory.CreateAnimal("Cat");
myCat.Speak();  // Outputs: Meow!
```

<details><summary>접기/펼치기</summary>

- Code
```cs
public interface IAnimal
{
    void Speak();
}

public class Dog : IAnimal
{
    public void Speak()
    {
        Console.WriteLine("Bark!");
    }
}

public class Cat : IAnimal
{
    public void Speak()
    {
        Console.WriteLine("Meow!");
    }
}

public static class AnimalFactory
{
   public static IAnimal CreateAnimal(string animalType)
   {
       switch (animalType)
       {
           case "Dog":
               return new Dog();
           case "Cat":
               return new Cat();
           default:
               throw new ArgumentException("Invalid animal type");
       }
   }
}
```

</details>

<br>


### 추상 팩토리 패턴 (Abstract Factory)
- 팩토리의 팩토리
- 추상 팩토리 패턴은 관련된 객체 그룹을 함께 생성해야 할 때 유용
- 시스템을 독립적으로 만들되, 여전히 유연성을 유지할 수 있게 합니다.
- 새로운 종류의 객체 집합을 쉽게 통합할 수 있도록 지원하며, 이로써 시스템의 확장성을 높이는 데 도움
```cs
IAnimalFactory dogFactory = new DogFactory();
IAnimal myDog = dogFactory.CreateANimal();
myDog.Speak();  // Outputs: Bark!
```

<br>
