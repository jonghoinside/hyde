### 01. 구조체란 무엇인가요? 😮

구조체(structure type)란 C언어에서 제공되는 기본 타입이 아닌 개발자가 새롭게 정의하는 사용자 정의 타입입니다. C언어에서 구조체는 멤버 변수들로 구성되며 C++ 에서는 멤버 함수까지도 포함하는 구조체, class에 대해서 배우게 됩니다. 지금은 C언어에서 구조체를 설명드리도록 하겠습니다.

### 02. 구조체 정의와 선언! 👊

구조체를 선언하는 방법을 알아보겠습니다.

```c
struct 구조체 이름 {
    멤버 변수 1;
    멤버 변수 2;
    ...
};
```

먼저 이 방법은 구조체의 멤버변수들을 정의했습니다. 구조체를 정의하고 바로 변수를 선언하는 방법도 있습니다.

```c
struct 구조체 이름 {
	멤버 변수 1;
	멤버 변수 2;
	...
} 구조체 변수 이름;
```

만약 구조체가 이미 정의되어 있고 C언어의 기본 타입처럼 선언해서 사용할 때는 이렇게 선언합니다.

```c
struct 구조체이름 구조체변수이름;
```

이 방법은 구조체 타입 변수를 만들 때마다 struct라는 키워드를 사용하여 구조체임을 명시해야 합니다. 하지만 typedef 키워드를 사용하여 구조체에 새로운 이름을 선언하면 매번 struct 키워드를 사용하지 않아도 됩니다. typedef 키워드를 사용한 선언은 아래와 같습니다.

```c
typedef struct (구조체 이름) {
    멤버 변수1;
    멤버 변수2;
    ...
} 구조체의 새로운 이름;

typedef struct 구조체이름 구조체의새로운이름;
```

구조체를 정의와 선언하는 문법에 대해 알아봤습니다. 예제를 활용해서 살펴보도록 하겠습니다.

### 03. 구조체는 왜 사용해야 하나요? 🙄

어떤 새로운 개념을 배우기 전에 항상 이 개념이 왜 필요한지에 대해 먼저 생각해보는 것이 중요합니다. 마찬가지로 구조체의 개념은 왜 생긴 것일까요? 간단하게 알아보겠습니다.

예를 들어 우리 반 학생들의 이름과 나이, 3판의 볼링 점수를 관리하는 프로그램을 만들어보겠습니다. 학생들의 정보는 이렇습니다.

- (name : 안종호, age : 28, scoreFirst : 100, scoreSecond : 150, scoreThird : 200, average : ?)
- (name : 박규화, age : 28, scoreFirst : 150, scoreSecond : 180, scoreThird : 90, average : ?)
- (name : 정성현, age : 28, scoreFirst : 200, scoreSecond : 120, scoreThird : 150, average : ?)
- (name : 오근재, age : 27, scoreFirst : 100, scoreSecond : 150, scoreThird : 180, average : ?)

저는 이 정보를 가지고 평균을 따로 구하고 그 평균값으로 순위를 나눠보고 싶습니다. 그리고 나이가 제일 어린 사람을 쉽게 찾아보고 싶습니다. 이 두가지의 목표를 위해서 자료를 저장하는 최적의 방법을 생각해봅시다.

우선 저장해야하는 data의 타입은 총 3가지입니다. 먼저는 name을 저장해야하기 때문에 char 배열이 있어야 하고, 나이와 점수를 저장하는 int, average는 double 타입으로 받아야 합니다.

그럼 아마도 이런 느낌의 변수의 종류가 있어야겠죠?

```c
char name[20];
int age;
int scoreFirst;
int scoreSecond;
int socreThird;
double average;
```

여기까지는 쉽게 생각할 수 있었습니다. 그런데 문제는 이제부터 어떻게 저장을 해야하나입니다. 각각의 이름별로 저 정보들을 따로 관리를 해야하는데 우리가 지금까지 배운 개념으로는 배열이 그나마 제일 효율적인 방법입니다. 그럼 저 정보들을 모두 배열로 변경하면 이렇게 됩니다.

```c
char name[4][20];
int age[4];
int scoreFirst[4];
int scoreSecond[4];
int socreThird[4];
double average[4];
```

자 이렇게 되면 이제 각 변수들의 배열 index를 이용해서 0일 때는 안종호, 1이면 박규화, 2는 정성현, 3은 오근재로 구분을 할 수 있게 되었습니다. 만약 average를 구하려면 어떻게 해야할까요?

```c
for (int i = 0 ; i < 4 ; ++i) {
    average[i] = (double)(scoreFirst[i] + scoreSecond[i] + scoreThird[i]) / 3;
}
```

만약 average를 함수를 정의해서 사용하는 방법을 사용하려면 average 함수의 인자값은 3개(첫번째 점수, 두번째 점수, 세번쨰 점수)를 받아야합니다. 만약 게임을 5판을 했다면 average 함수는 인자값을 5개 받아야 평균을 구할 수 있습니다. 무언가 조금씩 배열로 데이터를 저장하는 것이 비효율적이라고 생각드시지 않나요? 우리는 개발자 입장에서 data들이 index라는 기준으로 구별을 할 수 있지만 아주 효율적이지는 않습니다.

전체적인 입장에서 위의 데이터는 개개인의 볼링 점수라는 큰 틀에서 하나로 묶을 수 있을 겁니다. 서로 다른 data 타입의 묶음이 가능하게 만든 것이 바로 구조체(struct)입니다. 위에서 설명한 대로 구조체로 정의를 해보겠습니다. 개개인의 볼링 점수이므로 구조체의 이름은 BowlingScore로 묶어보겠습니다.

```c
struct BowlingScore {
    char name[20];
    int age;
    int scoreFirst;
    int scoreSecond;
    int socreThird;
    double average;
};
```

이렇게 묶였습니다. 만약 구조체를 정의하고 변수 이름을 바로 선언하기 위해서는

```c
struct BowlingScore {
    char name[20];
    int age;
    int scoreFirst;
    int scoreSecond;
    int socreThird;
    double average;
} entry;

//또는

struct BowlingScore {
    char name[20];
    int age;
    int scoreFirst;
    int scoreSecond;
    int socreThird;
    double average;
};

struct BowlingScore entry;
```

이렇게 구조체 변수를 선언할 수 있습니다. 그럼 평균을 구하기 위해서는 구조체 안의 점수가 들어있는 멤버 변수에 접근을 해야합니다. 접근하는 방법은 두 가지로 구조체 포인터 타입일 때와 구조체 타입일 때를 구분할 수 있습니다. 구조체 포인터 타입일 경우 안에 있는 멤버변수를 접근할 때 **->** 를 사용합니다. 구조체 타입일 때 접근하는 방법은 **.** 을 사용하여 접근합니다. 예를 들어 entry.scoreFirst 라고 접근할 수 있게 되는 겁니다. 그림을 통해 접근 방법에 대해 쉽게 이해시켜드리겠습니다.

<center><img src="/assets/images/posts/구조체(1).PNG" width="100%" height="100%"></center>

쉽게 정의하면 .(period) 또는 -> 연산자를 사용하기 전에 작성되는 변수의 이름의 타입이 포인터이면 -> 연산자를 value 면 .(period)를 사용하게 됩니다.

그럼 이제 구조체를 왜 사용해야하는지에 대해 생각해보았습니다. 간단하게 작성한 예제이지만 위의 볼링예제를 코드로 만들어보면 다음과 같습니다.

```c
#include <stdio.h>

struct BowlingScore {
    char name[20];
    int age;
    int scoreFirst;
    int scoreSecond;
    int scoreThird;
    double average;
};

void getAverage(struct BowlingScore* man) {
    man->average = (double)(man->scoreFirst + man->scoreSecond + man->scoreThird) / 3;
}

int main(void) {
    struct BowlingScore entry[4];
    
    
    for (int i = 0 ; i < 4 ; ++i) {
        printf("Input entry information(name, age, scoreFirst, scoreSecond, scoreThird) : ");
        scanf("%s %d %d %d %d", entry[i].name, &entry[i].age, &entry[i].scoreFirst, &entry[i].scoreSecond, &entry[i].scoreThird);
        getAverage(&entry[i]);
    }

    for (int i = 0 ; i < 4 ; ++i)
        printf("%s average score is %f\n", entry[i].name, entry[i].average);

    return 0;
}
```

위에서 작성한 4명의 정보를 각각 입력하면 각 사람 별로 평균 값이 계산되어 나오게 됩니다.

<center><img src="/assets/images/posts/구조체(2).PNG" width="100%" height="100%"></center>

예시로 만든 코드이지만 3판의 볼링 점수 계산 결과는 질문을 요청한 성현씨가 1등, 제가 2등이네요🙄 제가 만든거니까 제가 2등해도 괜찮죠? 😉 무튼 이런 간단한 아이디어를 가지고 예제를 짜보는 연습이 꼭 필요합니다!

예제를 만들고 나서 하나씩 기능을 추가하고 보완해가다보면 점점 더 완벽한 프로그램이 될 수 있으니까요! 예를 들어 저 위의 볼링 대회에 참가한 인원들의 3판의 점수로 평균을 구하는 예제에 순위대로 Sorting 해서 출력을 한다거나 매번 입력하는 것이 아닌 파일에 작성된 data를 읽어오게 하는 등의 기능을 추가하면 점점 실용성 있는 프로그램이 개발될 것입니다!

마지막으로 설명 안드린 부분이 하나 있는데요. 바로 typedef 함수에 관한 설명입니다. 간단하기 때문에 쉽게 이해하실 수 있습니다.

### (추가) typedef은? 🤨

typedef은 구조체에서 사용되었을 때 어떤 기능을 했는지 기억하시나요? 다시 위로 올라가서 살펴보면 typedef struct라고 선언한 구조체와 struct라고 선언한 구조체는 이후에 구조체 변수로 선언할 때 달라지는 모습을 볼 수 있었습니다. 바로 struct라는 키워드를 생략할 수 있었는데요. 바로 typedef 함수의 기능이 그렇습니다.

typedef은 반복해서 사용되는 코드로 인해 코드의 양이 많아지거나 복잡해질 경우 이를 간결하게 사용하기 위한 목적으로 사용됩니다. 함수 포인터에서 응용되는 경우도 있긴 하지만 그 부분을 지금 설명드리면 더 이해하기 어려우실 수도 있으니 생략하도록 하겠습니다. 이후에 typedef에 대한 이해가 높고 함수포인터에 대해 궁금해지셔서 요청주시면 추가로 설명 올려놓겠습니다.

간단하게 생략하면 typedef은 이름 그대로 type을 define한다. type 때문에 길어지는 코드를 새로운 이름으로 define 해서 사용할 수 있게 하는 것이 typedef의 기능이었습니다. 이렇게 구조체와 typedef에 대해 알아보았습니다. 설명 중에 더 궁금하신 부분이 있으시거나 이해가 어려운 부분을 댓글로 남겨주시면 추가 설명해드리겠습니다. 또 잘못된 부분이나 틀린 부분 있으면 꼭 댓글 남겨주세요! 감사합니다 👏

