# App development

Everything is a widget

Author

Benedict Thekkel

## Create a new Project

To create a new Flutter app, run the following commands in your shell or Terminal.

``` sh
flutter create test_flutter
```

``` sh
cd test_flutter
```

To verify that you have a running target device, run the following command.

``` sh
flutter devices
```

### **Open in Vscode and run the project from there**

### To run on emulator

List devices

``` sh
flutter emulators
```

Launch devices

``` sh
flutter emulators --launch <emulator id>
```

To run your app, run the following command.

``` sh
flutter run
```

## Make changes

- Open lib/main.dart.

- Make changes

- Save your changes.

- Type `r` in the terminal window.

## Widget types

### Stateless widget

- cannot change with time

### Stateful widget

- can change with time

#### initState()

- called only when the widget is created
- Subscribe to streams or any object that could change our widget data

#### Build()

- Builds the widget tree
- A build is triggered every time we use setState()

#### Dispose()

- When the widget/state object is removed

## Text Widget

- style
- textAlign
- overflow
- maxLin- etc

``` dart
Text('Click me')
```

## Button Widget

- color
- elevation
- disabledColor
- enabled
- etc

``` dart
     body: Center(
       child: ElevatedButton.icon(
         onPressed: () {
           print('You clicked me');
         },
         icon: const Icon(Icons.mail),
         label: const Text('Mail me'),
         style: ElevatedButton.styleFrom(
           shadowColor: Colors.amber,
         ),
       ),
     ),
```

## Row and Column Widget

``` dart
    body: Column(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        crossAxisAlignment: CrossAxisAlignment.center,
        children: <Widget>[
          Row(
            mainAxisAlignment: MainAxisAlignment.center,
            children: const <Widget>[
              Text('Hello'),
              Text('World'),
            ],
          ),
          Container(
            padding: const EdgeInsets.all(20.0),
            color: Colors.grey[200],
            child: const TextButton(
              onPressed: null,
              child: Text('Click Me'),
            ),
          ),
          const ElevatedButton(
            onPressed: null,
            child: Text('Click Me'),
          ),
          const OutlinedButton(
            onPressed: null,
            child: Text('Click'),
          ),
        ],
      ),
```

## Image Widget

``` dart
    body: Center(
        child: Image.asset('assets/beach1.jpg'),
      )
```

## Expanded Widget

> life flex grid

------------------------------------------------------------------------

``` dart
      body: Row(
        children: <Widget>[
          Expanded(
            flex: 3,
            child: Image.asset('assets/space1.jpg'),
          ),
          Expanded(
            flex: 2,
            child: Container(
              padding: const EdgeInsets.all(30.0),
              color: Colors.cyan,
              child: Text('1'),
            ),
          ),
          Expanded(
            flex: 1,
            child: Container(
              padding: const EdgeInsets.all(30.0),
              color: Colors.pink,
              child: Text('2'),
            ),
          ),
          Expanded(
            flex: 3,
            child: Container(
              padding: const EdgeInsets.all(30.0),
              color: Colors.amber,
              child: Text('3'),
            ),
          ),
        ],
      )
```

## Async functions

``` dart
void getData() async {
    // simulate network request for a username
    String username = await Future.delayed(Duration(seconds: 3), () {
      return 'yoshi';
    });

    // simulate network request to get bio of the username
    String bio = await Future.delayed(Duration(seconds: 2), () {
      return 'vegan, musician & egg collector';
    });

    print('$username - $bio');
  }
```

``` dart
  Future<void> getTime() async {
    Response response = await get(
      Uri.parse('http://worldtimeapi.org/api/timezone/$url'),
    );
    Map data = json.decode(response.body);

    String datetime = data['datetime'];
    String offset = data['utc_offset'].substring(1, 3);

    DateTime now = DateTime.parse(datetime);
    now = now.add(Duration(hours: int.parse(offset)));

    time = now.toString();
  }
}
```

## Routing

``` dart
      routes: {
        '/': (context) => Loading(),
        '/home': (context) => Home(),
        '/location': (context) => ChooseLocation(),
      },
```

``` dart
    Navigator.pushReplacementNamed(context, '/home', arguments: {
      'location': instance.location,
      'flag': instance.flag,
      'time': instance.time,
      'isDaytime': instance.isDaytime,
    });
```

``` dart
    onPressed: () async {
      dynamic result =
          await Navigator.pushNamed(context, '/location');
      setState(() {
        data = {
          'time': result['time'],
          'location': result['location'],
          'isDaytime': result['isDaytime'],
          'flag': result['flag'],
        };
      });
    },
```

``` dart
    Navigator.pop(context, {
      'location': instance.location,
      'flag': instance.flag,
      'time': instance.time,
      'isDaytime': instance.isDaytime,
    });
```

Back to top
