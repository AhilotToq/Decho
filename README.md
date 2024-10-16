#include <cs50.h>
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <math.h>

int count_letters(string text);
int count_words(string text);
int count_sentences(string text);
void print_grade_level(float index);

int main(void)
{
    string text = get_string("Text: ");

    int letters = count_letters(text);
    int words = count_words(text);
    int sentences = count_sentences(text);

    float L = (float) letters / words * 100;
    float S = (float) sentences / words * 100;

    float index = 0.0588 * L - 0.296 * S - 15.8;
    print_grade_level(index);
}

int count_letters(string text)
{
    int count = 0;
    for (int i = 0; text[i] != '\0'; i++)
    {
        if (isalpha(text[i]))
        {
            count++;
        }
    }
    return count;
}

int count_words(string text)
{
    int count = 0;
    bool in_word = false;
    for (int i = 0; text[i] != '\0'; i++)
    {
        if (isspace(text[i]))
        {
            in_word = false;
        }
        else if (!in_word)
        {
            in_word = true;
            count++;
        }
    }
    return count;
}

int count_sentences(string text)
{
    int count = 0;
    for (int i = 0; text[i] != '\0'; i++)
    {
        if (text[i] == '.' || text[i] == '!' || text[i] == '?')
        {
            count++;
        }
    }
    return count;
}

void print_grade_level(float index)
{
    int grade = round(index);

    if (grade < 1)
    {
        printf("Before Grade 1\n");
    }
    else if (grade >= 16)
    {
        printf("Grade 16+\n");
    }
    else
    {
        printf("Grade %d\n", grade);
    }
}

