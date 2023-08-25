# Calculatemygrade
This tool is made to calculate my GPA for Programming II

    using System;

    namespace GradeBookSimulator
     {
     class Program
     {
        static void Main(string[] args)
        {
            Console.WriteLine("Welcome to Cameron's Gradebook!");
            Console.WriteLine("Please enter your grades so that I can calculate your final grade.");
            Console.WriteLine();

            // Get quiz grades
            double[] quizGrades = GetGrades("Quizzes", 10);

            // Get exam grades
            double exam1Grade = GetGrade("Exam 1");
            double exam2Grade = GetGrade("Exam 2");

            // Get final paper grade
            double finalPaperGrade = GetGrade("Final Paper");

            // Calculate the final grade
            double finalGrade = CalculateFinalGrade(quizGrades, exam1Grade, exam2Grade, finalPaperGrade);

            Console.WriteLine();
            Console.WriteLine("Your final grade is: " + finalGrade.ToString("0.00"));
            Console.ReadLine();
        }

        static double[] GetGrades(string gradeType, int count)
        {
            double[] grades = new double[count];
            for (int i = 0; i < count; i++)
            {
                int quizNumber = i + 1;
                grades[i] = GetGrade(gradeType + " " + quizNumber);
            }
            return grades;
        }

        static double GetGrade(string gradeType)
        {
            double grade;
            bool validGrade = false;

            do
            {
                Console.Write("Enter the grade for " + gradeType + ": ");
                string input = Console.ReadLine();

                if (double.TryParse(input, out grade))
                {
                    if (grade >= 0 && grade <= 100)
                    {
                        validGrade = true;
                    }
                }

                if (!validGrade)
                {
                    Console.WriteLine("Invalid grade! Please enter a valid grade between 0 and 100.");
                }

            } while (!validGrade);

            return grade;
        }

        static double CalculateFinalGrade(double[] quizGrades, double exam1Grade, double exam2Grade, double finalPaperGrade)
        {
            // Calculate average quiz grade
            double quizAverage = CalculateAverage(quizGrades);

            // Calculate the final grade
            double finalGrade = (quizAverage * 0.25) + (exam1Grade * 0.25) + (exam2Grade * 0.25) + (finalPaperGrade * 0.25);
            return finalGrade;
        }

        static double CalculateAverage(double[] grades)
        {
            double sum = 0;
            foreach (double grade in grades)
            {
                sum += grade;
            }
            double average = sum / grades.Length;
            return average;
        }
    }
}
