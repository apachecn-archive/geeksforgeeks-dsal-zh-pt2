# 复数计算器的 C++程序

> 原文:[https://www . geesforgeks . org/c-复数计算器程序/](https://www.geeksforgeeks.org/c-program-for-complex-number-calculator/)

先决条件:[复数](https://www.geeksforgeeks.org/complex-numbers-c-set-1/)、数学、[面向对象编程](https://www.geeksforgeeks.org/object-oriented-programming-in-cpp/)

这是一个**复数计算器**，它执行下面提到的大量运算，以简化我们日常的数学问题。这个计算器的实现是使用 C++编程语言完成的，在 OOPs 中使用了运算符重载的概念。

**问题陈述:**

使用 C++编写一个程序来构建一个复数计算器，它可以执行以下操作:

**1。读复数:**要求用户输入复数的两个实数和虚数，对复数进行不同的运算。

```
Example:  Real Part value: 10
               Img Part value: 20
               Real Part value: 5
               Img Part value: 7
```

**2。显示复数:**如果用户在上述功能中输入了一个复数，则功能显示已经存在一个复数。

```
Example: Values are:
                    10+i20
                    5+i7
```

**3。** **复数相加:**它将两个复数相加，将第一个复数的实部加到第二个复数的实部，将第一个复数的虚部加到用户作为输入复数给出的第二个复数的虚部。

```
    Example: Addition is:
                    15+i27
```

**4。** **复数减法:**减去两个复数，第一个复数的实数部分减去第二个复数的实数部分，第一个复数的虚数部分减去用户作为输入复数给出的第二个复数的虚数部分。

```
Example: Subtraction is:
                    5+i13
```

**5。复数乘法:**将用户输入的两个复数相乘。

```
Example: Multiplication is:
                    -90+i170   
```

**6。** **复数除法:**将用户输入的两个复数相除。

```
Example:  Division is:
                     2.56757+i0.405405 
```

**7。** **复数的共轭:**它找到两个复数的共轭，这意味着它只改变用户作为输入复数给出的复数虚部的符号。

```
Example:  Conjugate is:
                    10-i20
                    5-i7 
```

**8。复数的正弦**:查找用户输入复数时给出的两个复数的正弦值。

```
Example:  Sin of 1st Complex Number is:
                     -1.3197e+008-i2.03544e+008
               Sin of 2nd Complex Number is:
                    -525.795+i155.537      
```

**9。复数的余弦:**求用户作为输入复数给出的两个复数的余弦值。

```
Example:   Cos of 1st Complex Number is:
                    -2.03544e+008+i1.3197e+008
               Cos of 2nd Complex Number is:
                     155.537+i525.794      
```

**10。复数的正切值:**查找用户作为输入复数给出的两个复数的正切值。

```
Example:   Tan of 1st Complex Number is:
                      7.75703e-018+i1
              Tan of 2nd Complex Number is:
                      -9.0474e-007+i1
```

**11 时。复数的正弦双曲:**它找到用户作为输入复数给出的两个复数的正弦双曲值。

```
Example:   Sinh of 1st Complex Number is:
                     4494.3+i10054.5
              Sinh of 2nd Complex Number is:
                     55.942+i48.7549
```

**12 时。复数的余弦双曲:**它找到用户作为输入复数给出的两个复数的余弦双曲值。

```
Example:  Cosh of 1st Complex Number is:
                   4494.3+i10054.5
            Cosh of 2nd Complex Number is:
                   55.947+i48.7505
```

**13。复数的正切双曲线:**它找到用户作为输入复数给出的两个复数的正切双曲线值。

```
Example:  Tanh of 1st Complex Number is:
                   1+i3.07159e-009
            Tanh of 2nd Complex Number is:
                    0.999988+i8.99459e-005
```

**14。复数的自然对数:**查找用户作为输入复数给出的两个复数的自然对数值。

```
Example:  log of 1st Complex Number is:
                   3.1073+i1.10715
           log of 2nd Complex Number is:
                   2.15203+i0.950547
```

**15。复数的范数:**求用户作为输入复数给出的两个复数的范数。

```
Example:  norm of 1st Complex Number is:
                  500+i0
           norm of 2nd Complex Number is:
                  74+i0
```

**16。复数的绝对值:**求两个复数的绝对值，意思是把负复数转化为正复数，正复数保持不变。

```
Example: Absolute of 1st Complex Number is:
                  22.3607+i0
           Absolute of 2nd Complex Number is:
                  8.60233+i0
```

**17。复数的自变量:**它找到用户作为输入复数给出的两个复数的自变量。

```
Example:  Argument of 1st Complex Number is:
                  1.10715+i0
           Argument of 2nd Complex Number is:
                   0.950547+i0
```

**18。复数的幂:**它找到用户作为输入复数给出的两个复数的幂。

```
Example:  power of 1st Complex Number is:
                  Enter Power: 2
                 -300+i400
           power of 2nd Complex Number is:
                 Enter Power: 3
                 -610+i182
```

**19。复数的指数:**它找到用户作为输入复数给出的两个复数的指数。

```
Example: Exponential of 1st Complex Number is:
                  8988.61+i20109
           Exponential of 2nd Complex Number is:
                 111.889+i97.5055
```

**20。复数的平方根:**它找到用户作为输入复数给出的两个复数的平方根。

```
Example: Square root of 1st Complex Number is:
                 4.02248+i2.48603
          Square root of 2nd Complex Number is:
                 2.6079+i1.34207
```

**21。显示复数的实部:**显示用户作为输入复数给出的两个复数的实部。

```
Example: Real Value of 1st Complex Number is: 10
          Real Value of 2nd Complex Number is: 5
```

**22。显示复数的虚部:**显示用户作为输入复数给出的两个复数的虚部。

```
Example: Imaginary Value of 1st Complex Number is: 20
          Imaginary Value of 2nd Complex Number is: 7
```

下面是上述方法的实现:

## C++

```
// Complex Number Calculator using C++
#include <cmath>
#include <complex>
#include <iostream>
using namespace std;
class com {
    // private variable declarations
    double reall, img;

public:
    // Method to read Complex Number
    void read()
    {
        // Reads Real Value of Complex Number
        cout << "Real Part value: ";
        cin >> reall;

        // Reads Imaginary Value of Complex Number
        cout << "Img Part value: ";
        cin >> img;
    }
    // display function declaration
    void display();

    //+ operator function declaration
    com operator+(com);

    //- operator function declaration
    com operator-(com);

    //* operator function declaration
    com operator*(com);

    // / operator function declaration
    com operator/(com);

    //~ operator function declaration
    com operator~(void);

    // sin_value function declaration
    com sin_value();

    // cos_value function declaration
    com cos_value();

    // tan_value function declaration
    com tan_value();

    // sinh_value function declaration
    com sinh_value();

    // cosh_value function declaration
    com cosh_value();

    // tanh_value function declaration
    com tanh_value();

    // log_value function declaration
    com log_value();

    // norm_value function declaration
    com norm_value();

    // abs_value function declaration
    com abs_value();

    // arg_value function declaration
    com arg_value();

    // power_value function declaration
    com power_value();

    // exp_value function declaration
    com exp_value();

    // sqrt_value function declaration
    com sqrt_value();

    // Declare inside com class and show Real part of
    // complex number
    double get_real()
    {
        // return real part
        return ((*this).reall);
    }
    // Declare inside com class and
    // show Imaginary part of complex number
    double get_img()
    {
        // return img part
        return ((*this).img);
    }
};
// Display Entered Complex Number
void com::display()
{
    // if imaginary part is positive then
    //  it display real + i img complex number
    if (img >= 0) {
        cout << reall << "+i" << img << endl;
    }

    // if imaginary part is negative then
    //  it display real - i img complex number
    else {
        cout << reall << "-i" << (-1) * img << endl;
    }
}
// Add two user entered complex number
com com::operator+(com o2)
{
    // declare temporary variable of class data type
    com temp;

    // add real part of two complex number
    //  and store in real part of temporary variable
    temp.reall = reall + o2.reall;

    // add imaginary part of two complex number
    //  and store in imaginary part of temporary variable
    temp.img = img + o2.img;

    // return temporary variable to function
    return temp;
}
// Subtract two user entered complex number
com com::operator-(com o2)
{
    // declare temporary variable of class data type
    com temp;

    // subtract real part of two complex number
    // and store in real part of temporary variable
    temp.reall = reall - o2.reall;

    // subtract imaginary part of two complex number and
    // store in imaginary part of temporary variable
    temp.img = img - o2.img;

    // return temporary variable to function
    return temp;
}
// Multiply two user entered complex number
com com::operator*(com o2)
{
    // declare temporary variable of class data type
    com temp;

    // Add Multiplication of  real part of two complex
    // number & imaginary part of two complex number and
    // store in real part of temporary variable
    temp.reall = (reall * o2.reall) + (-1 * (img * o2.img));

    // Add multiplication of real part of 1st and img part
    // of 2nd complex number and multiplication of img part
    // of 1st and real part of 2nd complex number and store
    // in real part of temporary variable
    temp.img = (img * o2.reall) + (reall * o2.img);

    // return temporary variable to function
    return temp;
}
// Divide two user entered complex number
com com::operator/(com o2)
{
    // declare temporary,o,num,den
    // variable of class data type
    com o, num, den, temp;

    // call conjugate function and perfor conjugate
    // operation
    o = ~o2;

    // calculate numerator and denominator complex number
    num = (*this) * (o);
    den = o2 * o;

    // divide numerator real part with denominator real part
    // and store in real part of temporay variable
    temp.reall = num.reall / den.reall;

    // divide numerator img part with denominator img part
    // and store in img part of temporay variable
    temp.img = num.img / den.reall;

    // return temporary variable to function
    return temp;
}
// find conjugate of both complex numbers
com com::operator~(void)
{
    // declare temporary variable of class data type
    com temp;

    // Store real part in real part of temporary variable
    temp.reall = reall;

    // Store multiplication of -1 and img in img part of
    // temporary variable to make conjugate
    temp.img = -1 * img;

    // return temporary variable to function
    return temp;
}
// find sine value of both complex numbers
com com::sin_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // sin() function find sin value of complex number
    sam = sin(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// find cosine value of both complex numbers
com com::cos_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // cos() function find cosin value of complex number
    sam = cos(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// find tangent value of both complex numbers
com com::tan_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // tan() function find tangent value of complex number
    sam = tan(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// find sine hyperbolic value of both complex numbers
com com::sinh_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // sinh() function find sine hyperbolic value of complex
    // number
    sam = sinh(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// find cosine hyperbolic value of both complex numbers
com com::cosh_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // cosh() function find cosine hyperbolic value of
    // complex number
    sam = cosh(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find tangent hyperbolic value of both complex numbers
com com::tanh_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // tanh() function find tangent hyperbolic value of
    // complex number
    sam = tanh(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find natural log value of both complex numbers
com com::log_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // log() function find natural log value of complex
    // number
    sam = log(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find Norm of both complex numbers
com com::norm_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // norm() function find Norm of complex number
    sam = norm(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find Absolute of both complex numbers
com com::abs_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // abs() function find Absolute of complex number
    sam = abs(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find Argument of both complex numbers
com com::arg_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // arg() function find Argument of complex number
    sam = arg(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find power of both complex numbers
com com::power_value(void)
{
    // declare variable p of integer data type
    int p;

    // Enter Power
    cout << "Enter Power: ";
    cin >> p;

    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // pow() function find Power of complex number
    sam = pow(cn, p);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find exponential of both complex numbers
com com::exp_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // exp() function find Exponential of complex number
    sam = exp(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
// it find Square root of both complex numbers
com com::sqrt_value(void)
{
    // declare temporary variable of class data type
    com temp;

    // declare cn and sam variable of complex data type
    complex<double> cn((*this).reall, (*this).img);
    complex<double> sam;

    // sqrt() function find Square Root of complex number
    sam = sqrt(cn);

    // real and img part of sam variable store in real and
    // img part of temporary variable
    temp.reall = real(sam);
    temp.img = imag(sam);

    // return temporary variable to function
    return temp;
}
int main()
{
    cout << "**********************Operations On Complex "
            "Number***************************";

    // Declare o1,o2 and o3 variable of class name data type
    com o1, o2, o3;

    // declare choice variable of integer type
    int choice;
    do {
        // Enter you choice to perform operation
        cout << "\nEnter Choice\n\n";
        cout << "1.Read Complex Number\n\n";
        cout << "2.Display Complex Number\n\n";
        cout << "3.Addition of Complex Number\n\n";
        cout << "4.Subtraction of Complex Number\n\n";
        cout << "5.Multiplication of Complex Number\n\n";
        cout << "6.Division of Complex Number\n\n";
        cout << "7.Conjugate of Complex Number\n\n";
        cout << "8.Sine of Complex Number\n\n";
        cout << "9.Cosine of Complex Number\n\n";
        cout << "10.Tangent of Complex Number\n\n";
        cout << "11.Sine Hyperbolic of Complex Number\n\n";
        cout
            << "12.Cosine Hyperbolic of Complex Number\n\n";
        cout << "13.Tangent Hyperbolic of Complex "
                "Number\n\n";
        cout << "14.Natural Log of Complex Number\n\n";
        cout << "15.Norm of Complex Number\n\n";
        cout << "16.Absolute of Complex Number\n\n";
        cout << "17.Argument of Complex Number\n\n";
        cout << "18.Power of Complex Number\n\n";
        cout << "19.Exponential of Complex Number\n\n";
        cout << "20.Square Root of Complex Number\n\n";
        cout << "21.Show Real Values of Complex Number\n\n";
        cout << "22.Show Imaginary Values of Complex "
                "Number\n\n";
        cout << "23.Exit\n\n";
        cin >> choice;
        cout << "\n";

        // use switch case according to user input
        switch (choice) {
        case 1:
            // Enter value of complex number
            cout << "Enter Values: \n";

            // call read() function
            o1.read();
            o2.read();
            break;
        case 2:
            cout << "Values are: \n";

            // call display function to display complex
            // number
            o1.display();
            o2.display();
            break;
        case 3:
            // call operator+() function to add complex
            // number
            o3 = o1 + o2;
            cout << "Addition is: \n";
            o3.display();
            break;
        case 4:
            // call operator-() function to subtract complex
            // number
            o3 = o1 - o2;
            cout << "Subtraction is: \n";
            o3.display();
            break;
        case 5:
            // call operator*() function to Multiply complex
            // number
            o3 = o1 * o2;
            cout << "Multiplication is: \n";
            o3.display();
            break;
        case 6:
            // call operator/() function to divide complex
            // number
            o3 = o1 / o2;
            cout << "Division is: \n";
            o3.display();
            break;
        case 7:
            // call operator~() function to Find conjugate of
            // complex number
            cout << "Conjugate is: \n";
            o3 = ~o1;
            o3.display();
            o3 = ~o2;
            o3.display();
            break;
        case 8:
            // call sin_value() function to Find sine value
            // of complex number
            cout << "Sin of 1st Complex Number is: \n";
            o3 = o1.sin_value();
            o3.display();
            cout << "Sin of 2nd Complex Number is: \n";
            o3 = o2.sin_value();
            o3.display();
            break;
        case 9:
            // call cos_value() function to Find cosine value
            // of complex number
            cout << "Cos of 1st Complex Number is: \n";
            o3 = o1.cos_value();
            o3.display();
            cout << "Cos of 2nd Complex Number is: \n";
            o3 = o2.cos_value();
            o3.display();
            break;
        case 10:
            // call tan_value() function to Find tangent
            // value of complex number
            cout << "Tan of 1st Complex Number is: \n";
            o3 = o1.tan_value();
            o3.display();
            cout << "Tan of 2nd Complex Number is: \n";
            o3 = o2.tan_value();
            o3.display();
            break;
        case 11:
            // call sinh_value() function to Find sine
            // hyperbolic value of complex number
            cout << "Sinh of 1st Complex Number is: \n";
            o3 = o1.sinh_value();
            o3.display();
            cout << "Sinh of 2nd Complex Number is: \n";
            o3 = o2.sinh_value();
            o3.display();
            break;
        case 12:
            // call cosh_value() function to Find cosine
            // hyperbolic value of complex number
            cout << "Cosh of 1st Complex Number is: \n";
            o3 = o1.cosh_value();
            o3.display();
            cout << "Cosh of 2nd Complex Number is: \n";
            o3 = o2.cosh_value();
            o3.display();
            break;
        case 13:
            // call tanh_value() function to Find tangent
            // hyperbolic value of complex number
            cout << "Tanh of 1st Complex Number is: \n";
            o3 = o1.tanh_value();
            o3.display();
            cout << "Tanh of 2nd Complex Number is: \n";
            o3 = o2.tanh_value();
            o3.display();
            break;
        case 14:
            // call log_value() function to Find log value of
            // complex number
            cout << "log of 1st Complex Number is: \n";
            o3 = o1.log_value();
            o3.display();
            cout << "log of 2nd Complex Number is: \n";
            o3 = o2.log_value();
            o3.display();
            break;
        case 15:
            // call norm_value() function to Find norm of
            // complex number
            cout << "norm of 1st Complex Number is: \n";
            o3 = o1.norm_value();
            o3.display();
            cout << "norm of 2nd Complex Number is: \n";
            o3 = o2.norm_value();
            o3.display();
            break;
        case 16:
            // call abs_value() function to Find absolute of
            // complex number
            cout
                << "Absolute of 1st Complex Number is: \n";
            o3 = o1.abs_value();
            o3.display();
            cout
                << "Absolute of 2nd Complex Number is: \n";
            o3 = o2.abs_value();
            o3.display();
            break;
        case 17:
            // call arg_value() function to Find argument of
            // complex number
            cout
                << "Argument of 1st Complex Number is: \n";
            o3 = o1.arg_value();
            o3.display();
            cout
                << "Argument of 2nd Complex Number is: \n";
            o3 = o2.arg_value();
            o3.display();
            break;
        case 18:
            // call power_value() function to Power norm of
            // complex number
            cout << "power of 1st Complex Number is: \n";
            o3 = o1.power_value();
            o3.display();
            cout << "power of 2nd Complex Number is: \n";
            o3 = o2.power_value();
            o3.display();
            break;
        case 19:
            // call exp_value() function to Find exponential
            // of complex number
            cout << "Exponential of 1st Complex Number is "
                    ": \n";
            o3 = o1.exp_value();
            o3.display();
            cout << "Exponential of 2nd Complex Number is "
                    ": \n";
            o3 = o2.exp_value();
            o3.display();
            break;
        case 20:
            // call sqrt_value() function to Find Square root
            // of complex number
            cout << "Square root of 1st Complex Number is "
                    ": \n";
            o3 = o1.sqrt_value();
            o3.display();
            cout << "Square root of 2nd Complex Number is "
                    ": \n";
            o3 = o2.sqrt_value();
            o3.display();
            break;
        case 21:
            // call get_real() function to get real part of
            // complex number
            cout << "Real Value of 1st Complex Number is: "
                 << o1.get_real() << endl;
            cout << "Real Value of 2nd Complex Number is: "
                 << o2.get_real() << endl;
            break;
        case 22:
            // call get_img() function to get imaginary part
            // of complex number
            cout << "Imaginary Value of 1st Complex Number "
                    "is: "
                 << o1.get_img() << endl;
            cout << "Imaginary Value of 2nd Complex Number "
                    "is: "
                 << o2.get_img() << endl;
            break;
        case 23:
            // it return 1 to do while() loop and stop
            // execution
            return 1;
            break;
        default:
            // if user enter invalid choice then it print
            // Enter valid option!!
            cout << "Enter valid option!!";
            break;
        }
    } while (1);
    return 0;
}
```

**输出视频:**

<video class="wp-video-shortcode" id="video-705414-1" width="640" height="360" preload="metadata" controls=""><source type="video/mp4" src="https://media.geeksforgeeks.org/wp-content/uploads/20211018174055/Complex-Number-Operation-Output.mp4?_=1">[https://media.geeksforgeeks.org/wp-content/uploads/20211018174055/Complex-Number-Operation-Output.mp4](https://media.geeksforgeeks.org/wp-content/uploads/20211018174055/Complex-Number-Operation-Output.mp4)</video>

**输出:**

> ******************复数上的操作********************
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> one
> 
> 输入值:
> 
> 实际零件值:10
> 
> Img 零件值:20
> 
> 实际零件值:5
> 
> Img 零件值:7
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Two
> 
> 值为:
> 
> 10+i20
> 
> 5+i7
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> three
> 
> 添加的内容是:
> 
> 15+i27
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> four
> 
> 减法是:
> 
> 5+i13
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> five
> 
> 乘法是:
> 
> -90+i170
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> six
> 
> 部门是:
> 
> 2.56757+i0.405405
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> seven
> 
> 共轭是:
> 
> 10-i20
> 
> 5-i7
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> eight
> 
> 第一复数的正弦为:
> 
> -1.3197e+008-i2.03544e+008
> 
> 第二复数的正弦为:
> 
> -525.795+i155.537
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> nine
> 
> 第一个复数的 Cos 为:
> 
> -2.03544e+008+i1.3197e+008
> 
> 第二个复数的 Cos 为:
> 
> 155.537+i525.794
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Ten
> 
> 第一复数的谭为:
> 
> 7.75703e-018+i1
> 
> 第二复数的谭为:
> 
> -9.0474e-007+i1
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Eleven
> 
> 第一个复数的 Sinh 为:
> 
> 4494.3+i10054.5
> 
> 第二复数的正弦为:
> 
> 55.942+i48.7549
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Twelve
> 
> 第一个复数的 Cosh 为:
> 
> 4494.3+i10054.5
> 
> 第二个复数的 Cosh 为:
> 
> 55.947+i48.7505
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Thirteen
> 
> 第一个复数的 Tanh 为:
> 
> 1+i3.07159e-009
> 
> 第二个复数的 Tanh 为:
> 
> 0.999988+i8.99459e-005
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Fourteen
> 
> 第一个复数的日志是:
> 
> 3.1073+i1.10715
> 
> 第二个复数的日志是:
> 
> 2.15203+i0.950547
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Fifteen
> 
> 第一复数的范数为:
> 
> 500+i0
> 
> 第二复数的范数为:
> 
> 74+i0
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Sixteen
> 
> 第一个复数的绝对值是:
> 
> 22.3607+i0
> 
> 第二复数的绝对值为:
> 
> 8.60233+i0
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Seventeen
> 
> 第一个复数的参数是:
> 
> 1.10715+i0
> 
> 第二个复数的自变量是:
> 
> 0.950547+i0
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Eighteen
> 
> 第一复数的幂是:
> 
> 输入功率:2
> 
> -300+i400
> 
> 第二复数的幂是:
> 
> 输入功率:3
> 
> -610+i182
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Nineteen
> 
> 第一个复数的指数为:
> 
> 8988.61+i20109
> 
> 第二复数的指数为:
> 
> 111.889+i97.5055
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Twenty
> 
> 第一个复数的平方根是:
> 
> 4.02248+i2.48603
> 
> 第二个复数的平方根是:
> 
> 2.6079+i1.34207
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Twenty-one
> 
> 第一个复数的实际值是:10
> 
> 第二个复数的实际值是:5
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> Twenty-two
> 
> 第一个复数的虚数是:20
> 
> 第二个复数的虚数是:7
> 
> 输入选择
> 
> 1.读取复数
> 
> 2.显示复数
> 
> 3.复数的加法
> 
> 4.复数的减法
> 
> 5.复数乘法
> 
> 6.复数除法
> 
> 7.复数的共轭
> 
> 8.复数的正弦
> 
> 9.复数的余弦
> 
> 10.复数的正切
> 
> 11.复数的正弦双曲
> 
> 12.复数的余弦双曲
> 
> 13.复数的正切双曲线
> 
> 14.复数的自然对数
> 
> 15.复数的范数
> 
> 16.复数的绝对值
> 
> 17.复数的论证
> 
> 18.复数的幂
> 
> 19.复数的指数
> 
> 20.复数的平方根
> 
> 21.显示复数的真实值
> 
> 22.显示复数的虚数
> 
> 23.出口
> 
> 23 
> 
> ——————————–
> 
> 进程在 94.69 秒后退出，返回值 1
> 
> 按任意键继续。。。