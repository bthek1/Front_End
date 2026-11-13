# Dart

https://dartpad.dev/

Author

Benedict Thekkel

## For loop

``` sh
void main() {
  for (int i = 0; i < 10; i++) {
    print('hello ${i + 1}');
  }
}
```

## Variables

### Integer

``` sh
void main() {
  int age = 30;
  print(age);
}
```

### String

``` sh
void main() {
  String name = 'ben';
  name = 'ken';
  print(name);
}
```

### Bool

``` sh
void main() {
  bool isNight = false;
  print(isNight);
}
```

### Dynamic variable

``` sh
void main() {
  dynamic name = 'ben';
  name = 30;
  print(name);
}
```

## Functions

``` sh
void main() {
  String greet = greeting();
  int age = getAge();
  print('${greet} and age:${age}');
}

String greeting() {
  return 'hello';
}

int getAge() {
  return 30;
}
```

## Function simplified

``` sh
void main() {
  String greet = greeting();
  int age = getAge();
  print('${greet} and age:${age}');
}

String greeting() => 'hello';

int getAge() => 30;
```

## List (array)

``` sh
void main() {
  List<String> names = ['ben', 'kim', 'charlie'];
  
  names.add('jeff');
  names.remove('kim');
  
  print(names);
}
```

## Classes

``` sh
void main() {
  User user1 = User('ben', 25);
  print(user1.username);
  user1.login();
}


class User {
  late String username;
  late int age;
  
  User(String name, int age){
    this.username = name;
    this.age = age;
  }
  
  void login() {
    print('user logged in');
  }
  
}
```

## Inheritance

``` sh
class SuperUser extends User {
  SuperUser(String username, int age):super(username, age);
    
  void publish() {
    print('Super user ${this.username}');
  }
}
```

Back to top
