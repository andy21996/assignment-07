/* ----------------------------------------------------------------------------
* Copyright &copy; 2015 Duy Nguyen <andy21996@csu.fullerton.edu>
* Released under the [MIT License] (http://opensource.org/licenses/MIT)
* ------------------------------------------------------------------------- */
* 
main.cpp
#include "Point.h"
#include "Point.cpp"

int main()
{
	double a1[] = { 5.2, 7.4 };
	double a2[] = { 10.2, 8.5 };
	Point<double, 2> p1(a1);
	Point<double, 2> p2(a2);

	cout << p1.distance(p2) << endl;

	cout << (p2 > p1) << endl;
	return 0;
}
Point.h
#ifndef POINT_H
#define POINT_H

#include <iostream>
#include <cmath>
using std::cout;
using std::endl;

template <typename T, const unsigned int SIZE>
class Point
{
private:
	T components_[SIZE];
public:
	Point();
	Point(T myCompononents[SIZE]);
	~Point();
	
	double distance(const Point& p) const;
	bool operator>(const Point& p) const;
	T operator[](int i) const;
};
#endif  // POINT_H
Point.cpp
#include "Point.h"

template <typename T, const unsigned int SIZE>
Point<T, SIZE>::Point()
{
	T filledValue = static_cast<T>(0.0);
	for (unsigned int i = 0; i < SIZE; i++)
		components_[i] = filledValue;
}

template <typename T, const unsigned int SIZE>
Point<T,SIZE>::Point(T myCompononents[SIZE])
{
	for (unsigned int i = 0; i < SIZE; i++)
		components_[i] = myCompononents[i];
}

template <typename T, const unsigned int SIZE>
Point<T, SIZE>::~Point() 
{
	
}

template <typename T, const unsigned int SIZE>
double Point<T, SIZE>::distance(const Point& p) const
{
	double sumPow = 0.0;
	for (unsigned int i = 0; i < SIZE; i++)
		sumPow += pow(components_[i] - p[i], 2);
	return sqrt(sumPow);
}

template <typename T, const unsigned int SIZE>
bool Point<T, SIZE>::operator>(const Point& p) const
{
	Point pointZero;
	return (this->distance(pointZero) > p.distance(pointZero));
}

template <typename T, const unsigned int SIZE>
T Point<T, SIZE>::operator[](int i) const
{
	return components_[i];
}
