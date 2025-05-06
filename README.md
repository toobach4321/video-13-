import 'package:flutter/material.dart';

void main() => runApp(BMICalculatorApp());

class BMICalculatorApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(home: BMICalculator());
  }
}

class BMICalculator extends StatefulWidget {
  @override
  _BMICalculatorState createState() => _BMICalculatorState();
}

class _BMICalculatorState extends State<BMICalculator> {
  double height = 160; // in cm
  double weight = 60;  // in kg
  double? _bmi;

  void _calculateBMI() {
    final heightInMeters = height / 100;
    setState(() {
      _bmi = weight / (heightInMeters * heightInMeters);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('BMI Calculator')),
      body: Padding(
        padding: const EdgeInsets.all(20),
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            Text('Height: ${height.toStringAsFixed(1)} cm'),
            Slider(
              value: height,
              min: 100,
              max: 220,
              onChanged: (val) => setState(() => height = val),
            ),
            SizedBox(height: 20),
            Text('Weight: ${weight.toStringAsFixed(1)} kg'),
            Slider(
              value: weight,
              min: 30,
              max: 150,
              onChanged: (val) => setState(() => weight = val),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: _calculateBMI,
              child: Text('Calculate BMI'),
            ),
            if (_bmi != null)
              Text('Your BMI is ${_bmi!.toStringAsFixed(2)}',
                  style: TextStyle(fontSize: 22, fontWeight: FontWeight.bold)),
          ],
        ),
      ),
    );
  }
}
