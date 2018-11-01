#include "Matrix.h"
#include <fstream>
#include <iostream>
#include <iomanip>
using namespace std;


///This constructor creates a matrix by passing to it the number of rows
///and the number of columns

Matrix:: Matrix(int row, int col)
    {
        this->row = row;
        this ->col = col;
        this->data = new int* [this->row];

        for (int i = 0; i < this->row; i++)
            this->data[i] = new int [this->col];
    }

///This constructor creates a matrix by passing to it the number of rows
///and the number of columns and the array containing the data

Matrix:: Matrix(int row, int col, int arr[]) :Matrix(row,col)
{
    for (int i = 0; i < this->row; i++)
        for (int j = 0; j < this->col; j++)
            this->data[i][j] = arr[i * col + j];
}

///This is the default constructor

Matrix:: Matrix(){
        this->row = 0;
        this-> col = 0;
    }


///This function returns the matrix

int** Matrix::getArr()
{
    return this->data;
}


///This function returns the rows

int Matrix::getrow()
    {
        return row;
    }

///This function returns the rows

int Matrix::getcol()
    {
        return col;
    }

///This function adds two matrices & returns the result in a new matrix

Matrix* Matrix:: operator + (Matrix& mat1)
    {
        Matrix* mat2 = new Matrix( this->row , this->col );

        if (this->row == mat1.row && this->col == mat1.col){
            for(int i=0; i<this->row; i++ ){
                for (int j=0; j<this->col; j++){
                    mat2->data[i][j] = this->data[i][j] + mat1.data[i][j];
                }
            }
            return mat2;
        }

        else{
            cout << "We can't add them as they don't have the same dimensions " <<endl;
        }
}

///This function subtracts two matrices & returns the result in a new matrix

Matrix* Matrix:: operator - (Matrix& mat1)
    {
        Matrix* mat2 = new Matrix( this->row , this->col );
        if (this->row == mat1.row && this->col == mat1.col){
        for(int i=0; i<this->row; i++ ){
            for (int j=0; j<this->col; j++){
                mat2->data[i][j] = this->data[i][j] - mat1.data[i][j];
            }

        }
            return mat2;
        }
        else{
            cout << "We can't subtract them as they don't have the same dimensions " <<endl;

        }
}

///This function multiplies two matrices & returns the result in a new matrix

Matrix* Matrix:: operator * (Matrix& mat1){

    Matrix* multiplication = new Matrix (this->row, mat1.col);

    if ( this->col == mat1.row )
    {
            for(int i = 0; i < this->row; ++i)
                for(int j = 0; j < mat1.col; ++j)
                {
                    multiplication->data[i][j]=0;
                }

        for(int i = 0; i < this->row; ++i)
            for(int j = 0; j < mat1.col; ++j)
                for(int k = 0; k < this->col; ++k)
                {
                    multiplication->data[i][j] += this->data[i][k] * mat1.data[k][j];
                }

        for(int i = 0; i < this->row; ++i)
            for(int j = 0; j < mat1.col; ++j)
            {
              // cout << " " << multiplication->data[i][j];

                if( j == mat1.col-1)
                    cout << endl;
            }

            }

    else
    {
        cout << "We can't multiply them as col1 not equal row2" <<endl;
    }
    return multiplication;
   }

///This function adds a scalar to the elements of a matrix & returns the result in a new matrix

  Matrix* Matrix:: operator + (int scalar)
{

    Matrix* add = new Matrix(this->row, this->col);

    for ( int i = 0; i < this->row; i++)
    {
        for ( int j = 0; j < this->col; j++)
        {
            add->data[i][j] = this->data[i][j]+scalar;
        }
    }
    return add;
}

///This function subtracts a scalar from the elements of a matrix & returns the result in a new matrix

 Matrix* Matrix:: operator - (int scalar)
{

    Matrix* sub = new Matrix (this->row, this->col);

    for ( int i = 0; i < this->row; i++)
    {
        for ( int j = 0; j < this->col; j++)
        {
            sub->data[i][j] = this->data[i][j]-scalar;
        }
    }
    return sub;
}

///This function multiplies a scalar by the elements of a matrix & returns the result in a new matrix

Matrix* Matrix:: operator * (int scalar){

    Matrix* multi = new Matrix (this->row, this->col);

    for ( int i = 0; i < this->row; i++)
    {
        for ( int j = 0; j < this->col; j++)
        {
            multi->data[i][j] = this->data[i][j]*scalar;
        }
    }
    return multi;

}

///This function adds 2 matrices and returns the result in the first matrix

Matrix* Matrix :: operator+= (Matrix& mat1)
{
    Matrix* addd = new Matrix (this->row, this->col);
    for (int i=0; i<this->row; i++)
    {
        for(int j=0; j<this->col; j++)
        {
            this->data[i][j]=this->data[i][j]+mat1.data[i][j];
            addd->data[i][j]=this->data[i][j];        }
    }
    return addd;
}

///This function subtracts 2 matrices and returns the result in the first matrix

Matrix* Matrix :: operator-= (Matrix& mat1)
{
    Matrix* subb = new Matrix (this->row, this->col);
    for (int i=0; i<this->row; i++)
    {
        for(int j=0; j<this->col; j++)
        {
            this->data[i][j]=this->data[i][j]-mat1.data[i][j];
            subb->data[i][j]=this->data[i][j];

        }
    }
    return subb;
}

///This function adds a scalar to a matrix and returns the result in the matrix

Matrix* Matrix :: operator+= (int scalar)
{
    Matrix* adddd = new Matrix (this->row, this->col);
    for (int i=0; i<this->row; i++)
    {
        for(int j=0; j<this->col; j++)
        {
        this->data[i][j]=this->data[i][j]+scalar;
        adddd->data[i][j]=this->data[i][j];
        }
    }
    return adddd;
}

///This function subtracts a scalar from a matrix and returns the result in the matrix

Matrix* Matrix :: operator-= (int scalar)
{
    Matrix* subbb = new Matrix (this->row, this->col);
    for (int i=0; i<this->row; i++)
    {
        for(int j=0; j<this->col; j++)
        {
            this->data[i][j]=this->data[i][j]-scalar;
            subbb->data[i][j]=this->data[i][j];

        }
    }
    return subbb;
}

///This function adds 1 to the elements of the matrix and returns the result in the same matrix

Matrix* Matrix :: operator++ ()
{
    Matrix* pluss = new Matrix (this->row, this->col);
    for(int i=0; i<this->row; i++)
    {
        for(int j=0; j<this->col; j++)
        {
            //mat.data[i][j]=++mat.data[i][j];
            ++this->data[i][j];
            pluss->data[i][j]=this->data[i][j];
        }
    }
    return pluss;

}

///This function subtracts 1 from the elements of the matrix and returns the result in the same matrix

Matrix* Matrix :: operator-- ()
{
    Matrix* minuss = new Matrix (this->row, this->col);
    for(int i=0; i<this->row; i++)
    {
        for(int j=0; j<this->col; j++)
        {
            //mat.data[i][j]=++mat.data[i][j];
            --this->data[i][j];
            minuss->data[i][j]=this->data[i][j];

        }
    }
    return minuss;
}

///This is the istream operator

istream& operator>> (istream& in , Matrix& object)
{
     int** arr = object.getArr();
     for(int i=0; i<object.getrow(); i++)
    {
        for(int j=0; j<object.getcol(); j++)
        {
            in >> arr[i][j];
        }
    }
    return in;
}

///This is the ostream operator

ostream& operator<< ( ostream& out , Matrix& object )
{
    int** arr = object.getArr();

    for ( int i = 0; i < object.getrow(); i++ )
    {
        for ( int j = 0; j < object.getcol(); j++ )
        {
            out << setw(6) << arr[i][j] << setw(6);
        }
        out << endl;
    }
    return out;
}

///This function checks if a matrix is a square matrix(# of rows==#of columns) or not

bool Matrix:: isSquare()
{
    bool check=true;
    if(this->row != this->col)
    {
        check=false;
    }
    return check;
}

///This function checks if a matrix is a symmetric matrix or not

bool Matrix:: isSymmetric()
{
     bool check=false;
    int counter=0;
    if(isSquare()==1){
        for(int i=0;i<this->row;i++){
            for(int j=0;j<this->col;j++){
                if(i != j && this->data[i][j]==this->data[j][i]){counter++;}
        }
    }
    if(counter==(this->row*this->col - this->row)){check=true;}
        }
    else{check=false;}
    return check;
}

///This function checks if a matrix is an identity matrix or not

bool Matrix:: isIdentity()
{
    bool check=false;
    if(isSquare()==1)
        for(int i=0; i<this->row; i++)
        {
            for(int j=0; j<this->col; j++)
            {
                if(i==j && this->data[i][j]!=1){check=false; break;}
                else if (i!=j && this->data[i][j]!=0 ){check=false; break;}
                else{check=true;}

            }
        }

    return check;
}

///This function checks if two matrices are equal or not

bool Matrix:: operator==(Matrix& mat1)
{
      bool check=true;
    if(this->row==mat1.row && this->col==mat1.col)
    {
        for(int i=0 ; i<this->row ; i++)
        {
            for(int j=0 ; j<this->col ; j++ )
            {
                if(this->data[i][j]!=mat1.data[i][j])
                {
                    check=false;

                }
            }
        }
    }
    return check;
}

///This function checks if two matrices are unequal or not

bool Matrix:: operator!=(Matrix& mat1)
{
    bool check=false;
    if(this->row != mat1.row || this->col != mat1.col)
    {
        check=true;
    }
    else
    {
        for(int i=0; i<this->row; i++)
        {
            for(int j=0; j<this->col; j++)
            {
                if(this->data[i][j] != mat1.data[i][j])
                {
                    check=true;
                }
                else
                {
                    check=false;
                }
            }
        }
    }
    return check;
}

///This function takes a matrix and returns its transpose

Matrix* Matrix::transpose()
{
    Matrix* matt= new Matrix(this-> col, this-> row);
     for(int i=0; i<matt->row; i++)
    {
        for(int j=0; j<matt->col; j++)
        {
            matt->data[i][j]=this->data[j][i];
        }
    }

    return matt;
}

///In this destructor, the object of the class(matrix) is deleted

Matrix::~Matrix()
{
    for ( int i = 0; i < this->row; i++ ) delete[] this->data[i];
    delete[] this->data;
}
