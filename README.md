IntroCsharp
===========
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace DesoCsharp
{
    class Program
    {
        static char movement(int[,] array,int score)
        {
            int N = 4, i, j;
            char move,end='e';
            if (END(array))
                return end;
            else 
            {
                Console.WriteLine("   Please choose movement!\n");
                Console.WriteLine("\t\t w - UP");
                Console.WriteLine("a - LEFT  \t s - DOWN  \t d - RIGHT\n");
                Console.WriteLine("Score:{0}\n", score);
                for (i = 0; i < N; i++)
                {
                    for (j = 0; j < N; j++)
                        Console.Write("   " + array[i, j] + "   ");
                    Console.WriteLine();
                }
                Console.Write("\n Move:");
                move = char.Parse(Console.ReadLine());
                return move;
            }
        }

        static void RandomNumber(int[,] array, Random rand)
        {
            int i, j, M = 4;
        here: i = rand.Next(M);
            j = rand.Next(M);
            if (array[i, j] == 0)
                array[i, j] = 2;
            else
                goto here;
        }

        static int MoveUP(int[,] array, Random rand, int score)
        {
            int red, kolona, N = 4, M = 3;
            for (red = M; red > 0; red--)
            {
                for (kolona = 0; kolona < N; kolona++)
                {
                    if (array[red, kolona] != 0)
                    {
                        if (array[red - 1, kolona] == 0)
                        {
                            array[red - 1, kolona] = array[red, kolona];
                            array[red, kolona] = 0;
                        }
                        if (array[red - 1, kolona] == array[red, kolona])
                        {
                            array[red - 1, kolona] = (array[red, kolona] * 2);
                            array[red, kolona] = 0;
                            score += 12;
                        }
                    }
                }
            }
            RandomNumber(array, rand);
            return score;
        }
        static int MoveDOWN(int[,] array, Random rand, int score)
        {
            int red, kolona, N = 4, M = 3;
            for (red = 0; red < M; red++)
            {
                for (kolona = 0; kolona < N; kolona++)
                {
                    if (array[red, kolona] != 0)
                    {
                        if (array[red + 1, kolona] == 0)
                        {
                            array[red + 1, kolona] = array[red, kolona];
                            array[red, kolona] = 0;
                        }
                        if (array[red + 1, kolona] == array[red, kolona])
                        {
                            array[red + 1, kolona] = (array[red, kolona] * 2);
                            array[red, kolona] = 0;
                            score += 12;
                        }
                    }
                }
            }
            RandomNumber(array, rand);
            return score;
        }

        static int MoveLEFT(int[,] array, Random rand,int score)
        {
            int red, kolona, N = 4, M = 3;
            for (red = 0; red < N; red++)
            {
                for (kolona = M; kolona > 0; kolona--)
                {
                    if (array[red, kolona] != 0)
                    {
                        if (array[red, kolona - 1] == 0)
                        {
                            array[red, kolona - 1] = array[red, kolona];
                            array[red, kolona] = 0;
                        }
                        if (array[red, kolona - 1] == array[red, kolona])
                        {
                            array[red, kolona - 1] = (array[red, kolona] * 2);
                            array[red, kolona] = 0;
                            score += 12;
                        }
                    }
                }
            }
            RandomNumber(array, rand);
            return score;
        }

        static int MoveRIGHT(int[,] array, Random rand, int score)
        {
            int red, kolona, N = 4, M = 3;
            for (red = 0; red < N; red++)
            {
                for (kolona = 0; kolona < M; kolona++)
                {
                    if (array[red, kolona] != 0)
                    {
                        if (array[red, kolona + 1] == 0)
                        {
                            array[red, kolona + 1] = array[red, kolona];
                            array[red, kolona] = 0;
                        }
                        if (array[red, kolona + 1] == array[red, kolona])
                        {
                            array[red, kolona + 1] = (array[red, kolona] * 2);
                            array[red, kolona] = 0;
                            score += 12;
                        }
                    }
                }
            }
            RandomNumber(array, rand);
            return score;
        }
        static bool END(int[,] array)
        {
            int i, j, N = 4, count = 0;
            bool flag = false;
            for (i = 0; i < N; i++)
            {
                for (j = 0; j < N; j++)
                {
                    if (array[i, j] != 0)
                        count++;
                }
            }
            Console.WriteLine("Free positions:{0}\n",(16 - count));     
            if (count == 16)
                flag = true;
            else
                flag = false;
            return flag;
        }

        static bool WIN(int[,] array)
        {
            int i, j, N = 4;
            bool win = false;
            for (i = 0; i < N; i++)
            {
                for (j = 0; j < N; j++)
                    if (array[i, j] == 2048)
                        win = true;
                    else
                        win = false;
            }
            return win;
        }

        static void Main(string[] args)
        {
            Random rand = new Random();
            int red, kolona, score = 0, i = 0, j = 0, N = 4, M = 3;
            char choice,end='e';
            char UP = 'w', DOWN = 's', LEFT = 'a', RIGHT = 'd';
            int[,] array = new int[N, N];
            do
            {
                red = rand.Next(M);
                kolona = rand.Next(M);
                array[red, kolona] = 2;
                i++;
            } while (i < M);
            Console.WriteLine("                     Welcome to my game 2048");
            Console.WriteLine("                          Made by Deso!");
            Console.WriteLine("                           Let's play...!!!\n\n");

        LOOP: choice = movement(array,score);
             if (choice == end)
            {
                Console.Clear();
                Console.WriteLine("\n  \t \t GAME OVER!!!\n");
            } 
            if ((choice != UP) && (choice != DOWN) && (choice != LEFT) && (choice != RIGHT) && (choice != end))
            {
                Console.Clear();
                goto LOOP;
            }
            
            if (choice == UP)
            {
                score = MoveUP(array, rand, score);
                if (WIN(array))
                {
                    Console.Clear();
                    Console.WriteLine("\n \t \t YOU WIN \n!!!");
                    Console.WriteLine("Score:{0}", score);
                }
                else
                {
                    Console.Clear();
                    goto LOOP;
                }
            }
            if (choice == DOWN)
            {
                 score = MoveDOWN(array, rand, score);
                if (WIN(array))
                {
                    Console.Clear();
                    Console.WriteLine("\n \t \t YOU WIN \n!!!");
                    Console.WriteLine("Score:{0}", score);
                }
                else
                {
                    Console.Clear();
                    goto LOOP;
                }
            }
            if (choice == LEFT)
            {
                score = MoveLEFT(array, rand, score);
                if (WIN(array))
                {
                    Console.Clear();
                    Console.WriteLine("\n \t \t YOU WIN \n!!!");
                    Console.WriteLine("Score:{0}", score);
                }
                else
                {
                    Console.Clear();
                    goto LOOP;
                }
            }
            if (choice == RIGHT)
            {
                score = MoveRIGHT(array, rand, score);
                if (WIN(array))
                {
                 Console.Clear();
                    Console.WriteLine("\n \t \t YOU WIN \n!!!");
                    Console.WriteLine("Score:{0}", score);
                }

                else
                {
                    Console.Clear();
                    goto LOOP;
                }
            }
        }

    }
}



     
