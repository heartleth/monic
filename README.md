# monic

    #include <iostream>
    using namespace std;
    
    @ main
        cout << "Hello, world!" << endl;
    @ endmain

monic 은 C++ 를 더 쉽게 쓸수 있도록 도와주는 도구입니다.

## 사용법

`monic file.monic` 을 cmd/powershell 셸에 입력하면 file.monic.cpp 로 변환됩니다

## .monic 파일

그냥 Cpp를 갖다 넣고 위의 명령을 실행하고 컴파일해도 잘 작동합니다. 하지만 `using namespace std;` 를 엏어주지 않으면 컴파일 에러가 나더군요.

`@ main` 과 `@ endmain` 으로 main 문을 열고 닫습니다.

## 아규먼트 식

`@ ~ $ 아규먼트식` 또는 `@ ! $ 아규먼트식` 으로 아규먼트식을 열고, `@ endarg` 로 아규먼트식을 닫습니다.
만얃 입력한 아규먼트식이 만족한다면 안의 내용을 실행합니다. 예를 들어, 

    #include <iostream>
    using namespace std;
    
    @ main
        @ ! $ <help>
            cout << "I'll help you to use Cpp easily";
        @ endarg
    @ endmain

를 적고 `monic file.monic` 을 실행하고 또 `file.monic.cpp`를 gcc 등으로 컴파일하고 `file --help` 를 실행하면 `I'll help you to use Cpp easily` 가 출력됩니다.

### @ ~ $ 와 @ ! $

아규먼트식을 아규먼트식 안에 작성할수도 있습니다.  
다른 아규먼트식을 덮기 위해 있는 것이 @ ~ $ 이고, 
더 덮지 않으려면 @ ! $ 를 사용해야 합니다.
예를 들어, 

    #include <iostream>
    using namespace std;
    
    @ ~ $ <help>
        @ ! $ * [me]
            cout << "I'll help you!";
        @ endarg
    @ endarg
    
를 exe로 컴파일한 뒤 `file --help me` 를 입력하면 `I'll help you!` 가 출력됩니다.

### <아규먼트>
<foo> 는 --foo 또는 -f 와 대응됩니다.

### [아규먼트]
안에 쓴 그대로와 대응됩니다.

### /아규먼트 정규식/
안에 쓴 정규식에 만족하는 것과 대응됩니다.

### %foo%
foo 라는 이름의 std::string에 저장됩니다.
즉 어떤 것을 써도 만족합니다.

### *
모든 것과 대응됩니다.
