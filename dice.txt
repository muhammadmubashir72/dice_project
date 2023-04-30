import 'package:flutter/material.dart';
import 'dart:math';

void main() {
  runApp(const DiceApp());
}

class DiceApp extends StatelessWidget {
  const DiceApp({super.key});

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Dice_Game',
        theme: ThemeData(primarySwatch: Colors.deepOrange),
        debugShowCheckedModeBanner: false,
        home: const HomePage());
  }
}

String Dice1 = "assets/dice1.png";
String Dice2 = "assets/dice1.png";
int count = 0;
int score = 0;

class HomePage extends StatefulWidget {
  const HomePage({super.key});

  @override
  State<HomePage> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  void _regenerate() {
    setState(() {
      count = 0;
      score = 0;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text(
          "Dice 10000 ",
          style: TextStyle(
              color: Color.fromARGB(255, 10, 201, 4),
              backgroundColor: Color.fromARGB(255, 146, 74, 6),
              fontSize: 40,
              decoration: TextDecoration.underline,
              fontWeight: FontWeight.bold,
              fontStyle: FontStyle.italic),
        ),
        centerTitle: true,
        backgroundColor: const Color.fromARGB(255, 160, 92, 4),
      ),
      body: Column(
        mainAxisAlignment: MainAxisAlignment.spaceEvenly,
        children: [
          // ignore: avoid_unnecessary_containers
        Align(alignment: Alignment.topRight,
         child: Container(
            child: Text("score : $score"),
          ),
          ),
           // ignore: avoid_unnecessary_containers
          Container(
            child: Text("count : $count"),
          ),
          Row(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: [
              Image.asset(Dice1, height: 125, width: 125),
              Image.asset(
                Dice2,
                height: 125,
                width: 125,
              )
            ],
          ),

          ElevatedButton(
              onPressed: () {
                setState(() {
                  count = count + 1;

                  int firstDice = Random().nextInt(6) + 1;
                  Dice1 = "assets/dice$firstDice.png";

                  int secondDice = Random().nextInt(6) + 1;
                  Dice2 = "assets/dice$secondDice.png";

                  if (firstDice == 1 && secondDice == 1 ||
                      firstDice == 6 && secondDice == 6) {
                    score = score + 10;
                  }
                });
              },
              child: const Text(
                "Press Dice",
                style: TextStyle(
                    fontSize: 40,
                    backgroundColor: Color.fromARGB(255, 187, 64, 19),
                    color: Color.fromARGB(255, 131, 238, 9),
                    fontStyle: FontStyle.italic),
              )),
                Visibility(
            visible: count >= 10,
            child: ElevatedButton(
              onPressed: _regenerate,
              child: const Text("Regenerate"),
            ),
            ),
        
        ],
      ),
    );
  }
}
