# Реквизиты
Виноградов Матвей Евгеньевич, 3 курс, z33434, 2023

# Наименование
[C++ & UNIX]: C++ BUILD / IF / LOOP, PYTHON

# Цель
Познакомить студента с принципами компиляции исходного кода. Составить программу с использованием циклов, условий и функций. Сравнить быстродействие между C++ и Python. Ознакомление с типами данных.

# Задача
1
[code.cpp] Создать и скомпилировать программу на C++
Результат сборки (компиляции) сохранять в папку build. Папку build сделать
игнорируемой для GIT. Программа должна получать на вход число – это
количество итераций для выполнения расчета. В рамках итерации выполнять
следующее вычисление: x ^2- x ^2+ x *4- x *5+ x + x . Вычисление выполнять в виде
отдельной от main функции, которая будет вызвана циклически из main.
Фиксировать время выполнения программы, затрачиваемое на расчет выражения
n раз (n задается в консоли перед вычислением). Предусмотреть дополнительный
цикл на повторную итерацию запуска программы вычислений. Если было введено
не число, то завершить выполнение программы.
2
[code.py] Создать и скомпилировать программу на Python 3
Результат сборки (компиляции) сохранять в папку build. Папку build сделать
игнорируемой для GIT. Программа должна получать на вход число – это
количество итераций для выполнения расчета. В рамках итерации выполнять
следующее вычисление: x ^2- x ^2+ x *4- x *5+ x + x . Вычисление выполнять в виде
отдельной от main функции, которая будет вызвана циклически из main.
Фиксировать время выполнения программы, затрачиваемое на расчет выражения
n раз (n задается в консоли перед вычислением). Предусмотреть дополнительный
цикл на повторную итерацию запуска программы вычислений. Если было введено
не число, то завершить выполнение программы.
3
[SAVE] Результат всех вышеперечисленных шагов сохранить в репозиторий
(+ отчет по данной ЛР в папку doc)
Фиксацию ревизий производить строго через ветку dev. С помощью скриптов
накатить ревизии на stg и на prd. Скрипты разместить в корне репозитория. Также
создать скрипты по возврату к виду текущей ревизии (даже если в папке имеются
несохраненные изменения + новые файлы).

# Решение
### 1. [code.cpp] Создать и скомпилировать программу на C++
Функция:
```c++
#include <cmath>
void step()
{
    pow(x,2)-pow(x,2)+pow(x,4)-pow(x,5)+x+x;
}
```
Чтение из входного потока:
```c++
int main()
{
    int n;
    cout << "Int: ";
    while (true) {
        if(cin >> n){
            cout << "n=" << n << "; solving..." << endl;
            for (int i = 0; i < n; i++)
            {
                step();
            }
            cout << "Int: ";
        } else {
            cout << "exit";
            break;
        }
    } 
    return 0;
}
```
Затраченное время:
```c++
#include <chrono>

auto begin = std::chrono::high_resolution_clock::now();
for (int i = 0; i < n; i++)
{
    step();
}
auto end = std::chrono::high_resolution_clock::now();
auto elapsed = std::chrono::duration_cast<std::chrono::nanoseconds>(end - begin);
```
Пример работы:
```text
Int: 10000
n=10000; solving...
time per step (us): 0.0621887
Int:
```

### 2. [code.py] Создать и скомпилировать программу на Python 3
```python
import time
x = 1
def step():
    x**2 - x**2 + x**4-x**5+x+x
    

if __name__ == '__main__':
    while True:
        try:
            n = int(input("Int: "))
            print(f"n={n}; solving...")
            begin = time.process_time()
            for _ in range(int(n)):
                step()
            end = time.process_time()
            elapsed = end - begin
            print(f'time per step (us): {elapsed/n * 1e6}')
        except ValueError:
            print("exit")
            break
```
Пример работы:
```text
Int: 10000
n=10000; solving...
time per step (us): 3.125
Int:
```
### 3. [SAVE] Результат всех вышеперечисленных шагов сохранить в репозиторий (+ отчет по данной ЛР в папку doc)
