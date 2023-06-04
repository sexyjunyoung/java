package ch09;

import java.awt.*;
import javax.swing.*;

public class Calculator extends JFrame {

    private JTextField display;
    private JLabel history;
    private JPanel panel;
    private double operand1, operand2, answer;
    private String operator;

    public Calculator() {
        this.setBounds(100, 100, 300, 500);
        this.setTitle("계산기");
        this.setLayout(new BorderLayout());

        display = new JTextField(30);
        display.setText("0");
        display.setFont(new Font("궁서체", Font.BOLD, 35));
        display.setHorizontalAlignment(SwingConstants.RIGHT);
        this.add(display, BorderLayout.NORTH);

        history = new JLabel("--");
        this.add(history, BorderLayout.SOUTH);

        panel = new JPanel();
        panel.setLayout(new GridLayout(6, 4));

        JButton button = new JButton("%");
        panel.add(button);

        button = new JButton("CE");
        panel.add(button);

        button = new JButton("C");
        button.addActionListener(e -> {
            display.setText("0");
        });
        panel.add(button);

        button = new JButton("<-");
        button.addActionListener(e -> {
            String text = display.getText();
            if (text.length() > 0) {
                display.setText(text.substring(0, text.length() - 1));
            }
        });
        panel.add(button);

        button = new JButton("1/x");
        button.addActionListener(e -> {
            double d = Double.parseDouble(display.getText());
            display.setText(1.0 / d + "");
        });
        panel.add(button);

        button = new JButton("x^2");
        button.addActionListener(e -> {
            double d = Double.parseDouble(display.getText());
            display.setText(d * d + "");
        });
        panel.add(button);

        button = new JButton("Sqrt");
        button.addActionListener(e -> {
            double d = Double.parseDouble(display.getText());
            display.setText(Math.sqrt(d) + "");
        });
        panel.add(button);

        button = new JButton("/");
        button.addActionListener(e -> {
            operand1 = Double.parseDouble(display.getText());
            operator = "/";
            display.setText("0");
        });
        panel.add(button);

        button = new JButton("7");
        button.addActionListener(e -> {
            appendToDisplay("7");
        });
        panel.add(button);

        button = new JButton("8");
        button.addActionListener(e -> {
            appendToDisplay("8");
        });
        panel.add(button);

        button = new JButton("9");
        button.addActionListener(e -> {
            appendToDisplay("9");
        });
        panel.add(button);

        button = new JButton("*");
        button.addActionListener(e -> {
            operand1 = Double.parseDouble(display.getText());
            operator = "*";
            display.setText("0");
        });
        panel.add(button);

        button = new JButton("4");
        button.addActionListener(e -> {
            appendToDisplay("4");
        });
        panel.add(button);

        button = new JButton("5");
        button.addActionListener(e -> {
            appendToDisplay("5");
        });
        panel.add(button);

        button = new JButton("6");
        button.addActionListener(e -> {
            appendToDisplay("6");
        });
        panel.add(button);

        button = new JButton("-");
        button.addActionListener(e -> {
            operand1 = Double.parseDouble(display.getText());
            operator = "-";
            display.setText("0");
        });
        panel.add(button);

        button = new JButton("1");
        button.addActionListener(e -> {
            appendToDisplay("1");
        });
        panel.add(button);

        button = new JButton("2");
        button.addActionListener(e -> {
            appendToDisplay("2");
        });
        panel.add(button);

        button = new JButton("3");
        button.addActionListener(e -> {
            appendToDisplay("3");
        });
        panel.add(button);

        button = new JButton("+");
        button.addActionListener(e -> {
            operand1 = Double.parseDouble(display.getText());
            operator = "+";
            display.setText("0");
        });
        panel.add(button);

        button = new JButton("+/-");
        button.addActionListener(e -> {
            String text = display.getText();
            if (!text.equals("0")) {
                if (text.startsWith("-")) {
                    display.setText(text.substring(1));
                } else {
                    display.setText("-" + text);
                }
            }
        });
        panel.add(button);

        button = new JButton("0");
        button.addActionListener(e -> {
            appendToDisplay("0");
        });
        panel.add(button);

        button = new JButton(".");
        button.addActionListener(e -> {
            String text = display.getText();
            if (!text.contains(".")) {
                display.setText(text + ".");
            }
        });
        panel.add(button);

        button = new JButton("=");
        button.addActionListener(e -> {
            operand2 = Double.parseDouble(display.getText());
            switch (operator) {
                case "+":
                    answer = operand1 + operand2;
                    break;
                case "-":
                    answer = operand1 - operand2;
                    break;
                case "*":
                    answer = operand1 * operand2;
                    break;
                case "/":
                    answer = operand1 / operand2;
                    break;
                default:
                    break;
            }
            display.setText(answer + "");
        });
        panel.add(button);

        this.add(panel, BorderLayout.CENTER);
        this.setDefaultCloseOperation(EXIT_ON_CLOSE);
        this.setVisible(true);
    }

    private void appendToDisplay(String text) {
        String currentText = display.getText();
        if (currentText.equals("0")) {
            display.setText(text);
        } else {
            display.setText(currentText + text);
        }
    }

    public static void main(String[] args) {
        new Calculator();
    }
}
