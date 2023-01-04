# CS50 notebook

## CS50网站、资料

- [manual pages to find CS50's libraries and functions](https://manual.cs50.io/)
- [C style from CS50](https://cs50.readthedocs.io/style/c/)

## CS50方法论

1. 看notes 2h
1. 看lecture 2.5h 推荐上用edx上的链接去YouTube看，而不是用edx自带的播放器，因为总是会卡
3. 看shorts 1.5h，shorts很重要，在作业里面经常会用到
4. 做lab（week2开始有） 时间不定
4. 做作业（尽量选择feel more comfortable的难度 ） 时间经常超过3小时

很多讲解非常形象，比如week0撕书，week3讲解merge sort时将字母从第0层sort到第三层得出复杂度nlogn

吐槽：week3的tideman作业一大堆选举规则，非常难，对于刚学的人不参考其他人的思路，卡好几天甚至几星期都有可能
## 小tips

atof()用于将字符串转换成双精度浮点数(double)




## 单词

heck 糟糕，见鬼

Exclamation 感叹号

Period 句号

Pedantically 卖弄学问地；学究式地，迂腐地

Trait 特质，特征

Round to the nearest integer 四舍五入到最近的整数

Retrace the steps 重溯以前的步骤

substitution cipher 替换密码

encrypt 把……加密，将……译成密码

conceal 隐藏；隐瞒

Divide and conquer 分而治之，各个击破

Zoom out 缩小

curly braces 花括号{}

on the order of 近似

Iterate 迭代

Resemble 类似

Prompt 促使

Shuffled 打乱的，洗牌

Elapsed 经过

Plurality 多数；复数；兼职；胜出票数

appointed by the monarch 由君主任命

First-past-the-post 最高票者当选

Ballot 选举

Head-to-head 白刃战

Margin 差距

glint 闪烁，发光

scan line 扫描线

precondition 前提，先决条件

equated with 相等于

wrap around to 环绕·

tinker with 胡乱地修补；tinker 小修补；笨手笨脚地做事

ampersand &记号名称(address operator)

asterisk *记号名称

toggle 切换，转换

allocate 分配

poke around 闲逛

whittle down 削弱

intimidating 令人望而生畏的

screw up 拧紧；鼓舞；弄糟

discipline 纪律，风纪；惩罚，处分；训导，管教

creep up 蠕升；渗上来

volatile 易变的

factorial 阶乘的

ephemeral 短暂的，短生的

companion 同伴，伴侣

grid 格栅 a grid of pixels

metadata 元数据

debute 首次参与,首次登台

tradeoff 权衡，折中

snippet 代码片段



## Assignments

### week1 mario-more

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int height, row, column, space;
    // Prompt user for height
    do
    {
        height = get_int("Enter Your Height: ");
    }
    while (height < 1 || height > 8);

    // For each row
    for (row = 0; row < height; row++)
    {
        // For each space
        for (space = 0; space < height - row - 1; space++)
        {
            printf(" ");
        }
        // For each column
        for (column = 0; column <= row; column++)
        {
            printf("#");
        }
        // Constant two spaces
        printf("  ");
        // The right part
        for (column = 0; column <= row; column++)
        {
            printf("#");
        }
        // Move to next row
        printf("\n");
    }

}
```

### week1 credit

```c
#include <stdio.h>
#include <cs50.h>

bool check_card(long card);
int get_length(long card);
bool checksum(long card);
void print_card_type(long card);

int main(void)
{
    long card_number;
    // Prompt user for credit card number
    do
    {
        card_number = get_long("Number: ");
    }
    while (card_number < 0);
    // Print card type
    if (check_card(card_number) == true)
    {
        print_card_type(card_number);
    }
    else
    {
        printf("INVALID\n");
    }
}
// Check card lenth and check sum
bool check_card(long card)
{
    int length = get_length(card);
    return (length == 13 || length == 15 || length == 16) && checksum(card);
}
// Get the length of credit card
int get_length(long card)
{
    int i;
    for (i = 0; card != 0; card /= 10, i++);
    return i;
}
// Check sum
bool checksum(long card)
{
    int sum = 0;
    int i;
    for (i = 0; card != 0; card /= 10, i++)
    {
        if (i % 2 == 0)
        {
            sum += card % 10;
        }
        else
        {
            int multiple = 2 * (card % 10);
            sum += multiple / 10 + multiple % 10;
        }
    }
    return (sum % 10) == 0;
}
// Identify and print card type
void print_card_type(long card)
{
    if ((card >= 34e13 && card < 35e13) || (card >= 37e13 && card < 38e13))
    {
        printf("AMEX\n");
    }
    else if (card >= 51e14 && card < 56e14)
    {
        printf("MASTERCARD\n");
    }
    else if ((card >= 4e12 && card < 5e12) || (card >= 4e15 && card < 5e15))
    {
        printf("VISA\n");
    }
    else
    {
        printf("INVALID\n");
    }
}
```





### week2 lab

思路：

1. 把一个单词所有的字母全部转换成大写

2. A对应的是65，所以相加的为word[i - 65]

   ```c
   #include <ctype.h>
   #include <cs50.h>
   #include <stdio.h>
   #include <string.h>
   
   // Points assigned to each letter of the alphabet
   int POINTS[] = {1, 3, 3, 2, 1, 4, 2, 4, 1, 8, 5, 1, 3, 1, 1, 3, 10, 1, 1, 1, 1, 4, 4, 8, 4, 10};
   
   int compute_score(string word);
   
   int main(void)
   {
       // Get input words from both players
       string word1 = get_string("Player 1: ");
       string word2 = get_string("Player 2: ");
   
       // Score both words
       int score1 = compute_score(word1);
       int score2 = compute_score(word2);
   
       // TODO: Print the winner
       if (score1 > score2)
       {
           printf("Player 1 wins!\n");
       }
       if (score1 < score2)
       {
           printf("Player 2 wins\n");
       }
       else
       {
           printf("Tie!\n");
       }
   }
   
   int compute_score(string word)
   {
       // TODO: Compute and return score for string
       int length = strlen(word);
       int sum = 0;
       for (int i = 0; i <length; i++)
       {
           word[i] = toupper(word[i]);
       }
   
       for (int j = 0; j < length; j++)
       {
           int m = (int)word[j]-65;
           sum = sum + POINTS[m];
       }
       return sum;
   }
   
   ```

   

### week2 readability

注意这道题中的计算结果是四舍五入的，四舍五入的巧妙方法是(int)(x + 0.5)

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int count_letters(string text);
int count_words(string text);
int count_sentences(string text);

int main(void)
{
    // prompt user for imput
    string input = get_string("Text: ");
    int letters = count_letters(input);
    int words = count_words(input);
    int sentences = count_sentences(input);
    // printf("%i letters\n", letters);
    // printf("%i words\n", words);
    // printf("%i sentences\n", sentences);
    // index = 0.0588 * L - 0.296 * S - 15.8
    double L = (double)letters / (double)words * 100;
    double S = (double)sentences / (double)words * 100;
    double index1 = 0.0588 * L - 0.296 * S - 15.8;
    int index = (int)(index1 + 0.5);
    // printf("L is %f\n", L);
    // printf("S is %f\n", S);
    // printf("index1 is %f\n", index1);
    // printf("index is %i\n",index);

    if (index >= 16)
    {
        printf("Grade 16+\n");
    }
    else if (index < 1)
    {
        printf("Before Grade 1\n");
    }
    else
    {
        printf("Grade %i\n", index);
    }
}

// count the number of letters in the text
int count_letters(string text)
{
    int count_of_letters = 0;
    int length = strlen(text);
    for (int i = 0; i < length; i++)
    {
        if (isalpha(text[i]))
        {
            count_of_letters = count_of_letters + 1;
        }
    }
    return count_of_letters;
}

// count the number of words in the text
int count_words(string text)
{
    int count_of_words = 1;
    int length = strlen(text);
    for (int i = 0; i < length; i++)
    {
        if (text[i] == ' ')
        {
            count_of_words = count_of_words + 1;
        }
    }
    return count_of_words;
}

// count the number of sentences in the text
int count_sentences(string text)
{
    int count_of_sentences = 0;
    int length = strlen(text);
    for (int i = 0; i < length; i++)
    {
        if (text[i] == '.')
        {
            count_of_sentences = count_of_sentences + 1;
        }
        else if (text[i] == '!')
        {
            count_of_sentences = count_of_sentences + 1;
        }
        else if (text[i] == '?')
        {
            count_of_sentences = count_of_sentences + 1;
        }
        else
        {
            count_of_sentences = count_of_sentences + 0;
        }
    }
    return count_of_sentences;
}
```

### week2 substitution

1. 原字母的大小写状态保留，且key有可能是大小混杂的，但是输出的大小写是以plain text为依据的
2. 只有alphabetical character需要被转换，其他的都不需要
3. 长度不正确（长于，小于）的可以要报error
4. 没有输入，需要报usage
5. 输入多个argv[]也需要报usage
6. 要有exit status直接退出程序

思路：

1. 先判断key是否符合原则
2. 再对plaintext分类讨论

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>
#include <ctype.h>

string encrypt(string text, string substitute);
bool check_duplicate(string text);
bool check_invalid(string text);

int main(int argc, string argv[])
{
    // check if there is no command-line argument
    if (argc == 1)
    {
        // if no command-line argument, exit
        printf("Usage: ./substitution key\n");
        return 1;
    }

    string key = argv[1];
    int length = strlen(key);

    // check whether the key is valid
    if (argc == 2)
    {
        if (length != 26)
        {
            // if length does not equal to 26, exit
            printf("Key must contain 26 characters.\n");
            return 1;
        }
        else if (check_duplicate(key))
        {
            // if there are duplicate characters, exit
            printf("Key must not contain duplicate characters.\n");
            return 1;
        }
        else if (check_invalid(key))
        {
            // if there are invalid characters, exit
            printf("Invalid character in key.\n");
            return 1;
        }
        else
        {
            // plain text should be provided and encrypted if the key is valid
            string plain_text = get_string("plaintext: ");
            string cipher_text = encrypt(plain_text, key);
            printf("ciphertext: %s\n", cipher_text);
            return 0;
        }
    }
    else
    {
        printf("Usage: ./substitution key\n");
        return 1;
    }
}

// implementation of substitution cipher
string encrypt(string text, string substitute)
{
    int text_len = strlen(text);
    int substitute_len = strlen(substitute);
    // convert all the letters of key to uppercase
    for (int i = 0; i < substitute_len; i++)
    {
        substitute[i] = toupper(substitute[i]);
    }
    // substitution
    for (int j = 0; j < text_len; j++)
    {
        if (text[j] >= 'A' && text[j] <= 'Z')
        {
            text[j] = substitute[(int)text[j] - 65];
        }
        else if (text[j] >= 'a' && text[j] <= 'z')
        {
            text[j] = substitute[(int)text[j] - 97] + 32;
        }
        else
        {
            text[j] = text[j];
        }
    }
    return text;
}

// check if there are duplicate characters
bool check_duplicate(string text)
{
    int text_len = strlen(text);
    int check = 0;
    for (int i = 0; i < text_len; i++)
    {
        for (int j = i + 1; j < text_len; j++)
        {
            if (text[i] == text[j])
            {
                check = check + 1;
            }
        }
    }
    return check != 0;
}

// check if there are invalid characters
bool check_invalid(string text)
{
    int text_len = strlen(text);
    int check2 = 0;
    for (int i = 0; i < text_len; i++)
    {
        if (isalpha(text[i]))
        {
            check2 = check2 + 0;
        }
        else
        {
            check2 = check2 + 1;
        }
    }
    return check2 != 0;
}
```

### week3 lab

```tex
sort1 uses: bubble sort

How do you know?: when sorting sorted50000.txt, bubble sort does not need to swap any of the numbers and just exits, so it should cost less than selection sort.

sort2 uses: merge sort

How do you know?: the time of sorting 50000 random numbers cost by sort2 algoritm is the smallest. Merge sort has the smallest big O when sorting large amount of numbers.

sort3 uses: selection sort

How do you know?: when sorting reversed50000.txt, selection sort should cost less than the bubble sort.

```

### week3 plurality

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// Candidates have name and vote count
typedef struct
{
    string name;
    int votes;
}
candidate;

// Array of candidates
candidate candidates[MAX];

// Number of candidates
int candidate_count;

// Function prototypes
bool vote(string name);
void print_winner(void);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: plurality [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i].name = argv[i + 1];
        candidates[i].votes = 0;
    }

    int voter_count = get_int("Number of voters: ");

    // Loop over all voters
    for (int i = 0; i < voter_count; i++)
    {
        string name = get_string("Vote: ");

        // Check for invalid vote
        if (!vote(name))
        {
            printf("Invalid vote.\n");
        }
    }

    // Display winner of election
    print_winner();
}

// Update vote totals given a new vote
bool vote(string name)
{
    int b = 0;
    for (int i = 0; i < candidate_count; i++)
    {
        if (strcmp(candidates[i].name, name) == 0)
        {
            candidates[i].votes = candidates[i].votes + 1;
            b = b + 1;
            return true;
        }
    }

    return b != 0;
}

// Print the winner (or winners) of the election
void print_winner(void)
{
    int max = candidates[0].votes;

    for (int i = 1; i < candidate_count; i++)
    {
        if (candidates[i].votes > max)
        {
            max = candidates[i].votes;
        }
    }

    for (int i = 0; i < candidate_count; i++)
    {
        if (candidates[i].votes == max)
        {
            printf("%s\n", candidates[i].name);
        }
    }

}
```



### week3 tideman

储存名字的是 string candidates[]

名字的数量是 candidate_count

ranks[]里面储存名次

bool vote:

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// preferences[i][j] is number of voters who prefer i over j
int preferences[MAX][MAX];

// locked[i][j] means i is locked in over j
bool locked[MAX][MAX];

// Each pair has a winner, loser
typedef struct
{
    int winner;
    int loser;
}
pair;

// check whether the edges will create a cycle
bool check_cycle(int winner, int loser);

// Array of candidates
string candidates[MAX];
pair pairs[MAX * (MAX - 1) / 2];

int pair_count;
int candidate_count;

// Function prototypes
bool vote(int rank, string name, int ranks[]);
void record_preferences(int ranks[]);
void add_pairs(void);
void sort_pairs(void);
void lock_pairs(void);
void print_winner(void);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: tideman [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i] = argv[i + 1];
    }

    // Clear graph of locked in pairs
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = 0; j < candidate_count; j++)
        {
            locked[i][j] = false;
        }
    }

    pair_count = 0;
    int voter_count = get_int("Number of voters: ");

    // Query for votes
    for (int i = 0; i < voter_count; i++)
    {
        // ranks[i] is voter's ith preference
        int ranks[candidate_count];

        // Query for each rank
        for (int j = 0; j < candidate_count; j++)
        {
            string name = get_string("Rank %i: ", j + 1);

            if (!vote(j, name, ranks))
            {
                printf("Invalid vote.\n");
                return 3;
            }
        }

        record_preferences(ranks);

        printf("\n");
    }

    add_pairs();
    sort_pairs();
    lock_pairs();
    print_winner();
    return 0;
}

// Update ranks given a new vote
bool vote(int rank, string name, int ranks[])
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (strcmp(candidates[i], name) == 0)
        {
            ranks[rank] = i;
            return true;
        }
    }
    return false;
}

// Update preferences given one voter's ranks
void record_preferences(int ranks[])
{
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = i + 1; j < candidate_count; j++)
        {
            preferences[ranks[i]][ranks[j]]++;
        }
    }
    return;
}

// Record pairs of candidates where one is preferred over the other
void add_pairs(void)
{
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = i + 1; j < candidate_count; j++)
        {
            if (preferences[i][j] > preferences[j][i])
            {
                pairs[pair_count].winner = i;
                pairs[pair_count].loser = j;
                pair_count = pair_count + 1;
            }
            else if (preferences[i][j] < preferences[j][i])
            {
                pairs[pair_count].winner = j;
                pairs[pair_count].loser = i;
                pair_count = pair_count + 1;
            }
        }
    }
    return;
}

// Sort pairs in decreasing order by strength of victory
void sort_pairs(void)
{
    bool swapped;
    for (int i = 0; i < pair_count - 1; i++)
    {
        swapped = false;
        for (int j = 0; j < pair_count - 1; j++)
        {
            if (preferences[pairs[j].winner][pairs[j].loser] < preferences[pairs[j + 1].winner][pairs[j + 1].loser])
            {
                pair temp = pairs[j];
                pairs[j] = pairs[j + 1];
                pairs[j + 1] = temp;
                swapped = true;
            }
        }
        if (swapped == false)
        {
            break;
        }
    }
    return;
}

// Lock pairs into the candidate graph in order, without creating cycles
void lock_pairs(void)
{
    for (int i = 0; i < pair_count; i++)
    {
        if (!check_cycle(pairs[i].loser, pairs[i].winner))
        {
            locked[pairs[i].winner][pairs[i].loser] = true;
        }
    }
    return;
}

// Print the winner of the election
void print_winner(void)
{
    for (int i = 0; i < candidate_count; i++)
    {
        int locked_edge_numbers = 0;
        for (int j = 0; j < candidate_count; j++)
        {
            if (locked[j][i] == false)
            {
                locked_edge_numbers++;
                if (locked_edge_numbers == candidate_count)
                {
                    printf("%s\n", candidates[i]);
                }
            }
        }
    }
    return;
}

// check whether the edges will create a cycle
bool check_cycle(int loser, int winner)
{
    if (loser == winner)
    {
        return true;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        if (locked[loser][i])
        {
            if (check_cycle(i, winner))
            {
                return true;
            }
        }
    }
    return false;
}

bool cycle(int end, int cycle_start)
{
    // Return True if there is a cycle created (recursion base case)
    if (end == cycle_start)
    {
        return true;
    }
    // Loop through candidates
    for (int i = 0; i < candidate_count; i++)
    {
        if (locked[end][i])
        {
            if (cycle(i, cycle_start))
            {
                return true;
            }
        }
    }
    return false;
}

```

### week4 lab

```c
// Modifies the volume of an audio file

#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

// Number of bytes in .wav header
const int HEADER_SIZE = 44;

// Create an array to store header file
uint8_t header[HEADER_SIZE];

// using the int16_t type to store audio sample
int16_t buffer;

int main(int argc, char *argv[])
{
    // Check command-line arguments
    if (argc != 4)
    {
        printf("Usage: ./volume input.wav output.wav factor\n");
        return 1;
    }

    // Open files and determine scaling factor
    FILE *input = fopen(argv[1], "r");
    if (input == NULL)
    {
        printf("Could not open file.\n");
        return 1;
    }

    FILE *output = fopen(argv[2], "w");
    if (output == NULL)
    {
        printf("Could not open file.\n");
        return 1;
    }

    float factor = atof(argv[3]);

    // TODO: Copy header from input file to output file
    fread(&header, sizeof(header), 1, input);
    fwrite(&header, sizeof(header), 1, output);

    // TODO: Read samples from input file and write updated data to output file
    while (fread(&buffer, sizeof(buffer), 1, input))
    {
        buffer *= factor;
        fwrite(&buffer, sizeof(buffer), 1, output);
    }
    // Close files
    fclose(input);
    fclose(output);
}

```

### week4 filter-more



```c
#include "helpers.h"
#include <math.h>

// Convert image to grayscale
void grayscale(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            int average = round((image[i][j].rgbtRed + image[i][j].rgbtGreen + image[i][j].rgbtBlue) / 3.0);
            image[i][j].rgbtRed = average;
            image[i][j].rgbtBlue = average;
            image[i][j].rgbtGreen = average;
        }
    }
    return;
}

// Reflect image horizontally
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
    for (int i = 0; i < height; i++)
    {
        if (width % 2 == 1)
        {
            for (int j = 0; j < ((width + 1) / 2) - 1; j ++)
            {
                RGBTRIPLE replace[i][j];
                replace[i][j] = image[i][j];
                image[i][j] = image[i][width - 1 - j];
                image[i][width - 1 - j] = replace[i][j];
            }
        }
        else
        {
            for (int j = 0; j < width / 2; j ++)
            {
                RGBTRIPLE replace[i][j];
                replace[i][j] = image[i][j];
                image[i][j] = image[i][width - 1 - j];
                image[i][width - 1 - j] = replace[i][j];
            }
        }
    }
    return;
}

// Blur image
void blur(int height, int width, RGBTRIPLE image[height][width])
{
    RGBTRIPLE replace[height][width];
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            float blueSum = 0;
            float greenSum = 0;
            float redSum = 0;
            float counter = 0;
            for (int x = i - 1; x < i + 2; x++)
            {
                for (int y = j - 1; y < j + 2; y++)
                {
                    if (x < 0 || x > height - 1)
                    {
                        continue;
                    }
                    if (y < 0 || y > width - 1)
                    {
                        continue;
                    }
                    blueSum += image[x][y].rgbtBlue;
                    greenSum += image[x][y].rgbtGreen;
                    redSum += image[x][y].rgbtRed;
                    counter++;
                }
            }
            replace[i][j].rgbtBlue = round(blueSum / counter);
            replace[i][j].rgbtGreen = round(greenSum / counter);
            replace[i][j].rgbtRed = round(redSum / counter);
        }
    }
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            image[i][j].rgbtBlue = replace[i][j].rgbtBlue;
            image[i][j].rgbtGreen = replace[i][j].rgbtGreen;
            image[i][j].rgbtRed = replace[i][j].rgbtRed;
        }
    }
    return;
}

// Detect edges
void edges(int height, int width, RGBTRIPLE image[height][width])
{
    RGBTRIPLE replace[height][width];
    int kernelX[3][3] = {{-1, 0, 1}, {-2, 0, 2}, {-1, 0, 1}};
    int kernelY[3][3] = {{-1, -2, -1}, {0, 0, 0}, {1, 2, 1}};
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            int gxBlue = 0;
            int gyBlue = 0;
            int gxGreen = 0;
            int gyGreen = 0;
            int gxRed = 0;
            int gyRed = 0;
            for (int x = i - 1; x < i + 2; x++)
            {
                for (int y = j - 1; y < j + 2; y++)
                {
                    if (x < 0 || x > height - 1)
                    {
                        continue;
                    }
                    if (y < 0 || y > width - 1)
                    {
                        continue;
                    }
                    gxBlue += image[x][y].rgbtBlue * kernelX[x - i + 1][y - j + 1];
                    gyBlue += image[x][y].rgbtBlue * kernelY[x - i + 1][y - j + 1];
                    gxGreen += image[x][y].rgbtGreen * kernelX[x - i + 1][y - j + 1];
                    gyGreen += image[x][y].rgbtGreen * kernelY[x - i + 1][y - j + 1];
                    gxRed += image[x][y].rgbtRed * kernelX[x - i + 1][y - j + 1];
                    gyRed += image[x][y].rgbtRed * kernelY[x - i + 1][y - j + 1];
                }
            }
            // calculate Sobel operator
            int blue = round(sqrt(gxBlue * gxBlue + gyBlue * gyBlue));
            int green = round(sqrt(gxGreen * gxGreen + gyGreen * gyGreen));
            int red = round(sqrt(gxRed * gxRed + gyRed * gyRed));
            // cap at 255
            if (blue > 255)
            {
                blue = 255;
            }
            if (green > 255)
            {
                green = 255;
            }
            if (red > 255)
            {
                red = 255;
            }
            replace[i][j].rgbtBlue = blue;
            replace[i][j].rgbtGreen = green;
            replace[i][j].rgbtRed = red;
        }
    }
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            // assign new values to pixels
            image[i][j].rgbtBlue = replace[i][j].rgbtBlue;
            image[i][j].rgbtGreen = replace[i][j].rgbtGreen;
            image[i][j].rgbtRed = replace[i][j].rgbtRed;
        }
    }


    return;
}

```

### week4 recover

```c


#include<stdio.h>
#include <stdlib.h>




int main(int argc, char *argv[])
{
    //Make sure that you have one command line argument
    if (argc != 2)
    {
        printf( "Please enter file to open.\n");
        return 1;
    }

// open memory card file
FILE *file=fopen(argv[1],"r");
if(file == NULL)
{ 
    printf("not a file\n");
}

// set jpg count
int jpg_found=0;

// set filecount
int filecount=0;

// set buffer with 512 bytes. 
unsigned char buffer[512]; // alternate : unsigned char buffer[BUFFER_SIZE]  but you have to :#define BUFFER_SIZE 512 at top

// define file for images
FILE *img=NULL;

// set filename 
char filename[8]; // 8= 3 digits(000-049) 1 dot 3 char(jpg) 1 /0(null terminating char)

// read file
while(fread(buffer,512,1,file)==1) // data,size,qty,file; while this condition is satisfied

// check if jpg using 1st four bytes
 {
 if (buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff && (buffer[3] & 0xf0) == 0xe0) // for buffer[3] condition watch walkthrough video explanation
{
if( jpg_found==1) // already opened a prior jpg byte then close it
{
    fclose(img);
}
else // if not then you found a jpeg so increment counter
{ 
    jpg_found=1;
}

sprintf(filename,"%03i.jpg",filecount); // print filename 000.jpg and increasing each time
img=fopen(filename,"w"); // open file for images to append/write 
filecount++; // after each file is opened increment file count counter
}
if(jpg_found==1) // once found jpeg write from buffer to img file 
{
    fwrite(&buffer,512,1,img);
}
}
fclose(file); // close file(memory card to buffer) and img(buffer to img file)
fclose(img);

// done
return 0;

}
```









## WEEK 2 Arrays

### compiling

Compiling source codes into machine codes is actually made up of four smaller steps:

- preprocessing
- compiling
- assembling
- linking

preprocessing: replacing the lines that starts with a #.

Exp. #include <cs.50> will tell clang to look for that header file, because it contains content, such as prototypes of functions.

Compiling: taking our source code in C and converting it into assembly language

Assembling: take the code in assemble and translate it into binary.

Compiling: combine the compiled libraries and compiled binary of our program 



### debugging

1. use printf
2. There is a debugger in VS code: red dot or called breakpoint Debug50 ./filename
3. rubber duck  talk to it

```c
#include <cs50.h>
#include <stdio.h>

int get_negative_int(void);
  
int main(void)
{
  int i = get_negative_int();
  printf("%i\n",i);
}

int get_negative_int(void)
{
  int n;
  do
  {
    n = get_int("waht's the number: ");
  }
  while (n >= 0);
  return n;
}
```



### memory

Bool: 1byte

Char: 1byte (8bits in 1 byte), by ASCII 256 different characters can be represented

Double: 8 bytes

Float: 4bytes

int: 4bytes

Long: 8bytes

String: variable

RAM: random-access memory, stores zeroes and ones 

### arrays

Declaration: tepe name[size]

Float lechi[50]

```c
bool truthtable[3] = { false, false, true};
```

```c
bool battleship[10][10];
```

在C里面，将一个array复制到另一个时，不能直接用=赋值，而是要用loop

整个array不是一个variable，但是array里的每个element是一个变量

```c
int foo[3] = {1, 2, 3};
int bar[3];

for (int j = 0; j < 3; j++)
{
bar[j] = int[j];
}

```



Square bracket: [ ]

It turns out we can refer to multiple variables with one name with another type called an **array**

**Array is 0-indexed**

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    int n = get_int("How many scores? ");
  
  	int scores[n];

    for (int i = 0; i < n; i++)
    {
      scores[i] = get_int("Score: ");
    }

    printf("Average: %f\n", (scores[0] + scores[1] + scores[2]) / 3.0);
} 
```



### characters

We can explicitly convert chars to ints by:

```c
printf("i%i%i%\n", (int)c1, (int)c2, (int)c3);
```



### strings

Strings are actually just arrays of characters 

```c
    string s = "HI!";
    printf("%i %i %i %i\n", s[0], s[1], s[2], s[3]);
```

the output is 72 73 33 0

In C, strings end with a sopecial chatacter '\0', so 4 bytes are needed to store a string with 3 bytes.

Eight 0s called NUL

**a program to capitalize the letters in a string: **

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

int main()void
{
  string name = get_string("your name in lower case: ");
  for (int i = 0, n = strlen(name); i < n; i++)
  {
    if ( s[i] >= 'a' && s[i] <= 'z')
    {
      printf("%c", s[i] - 32);
    }
    else
    {
      printf("%c", s[i]);
    }
  }
}
```



### small tips to improve the loop

Use:

```c
for (int i = 0, n = strlen(s); i < n; i++)
```

Rather than:

```c
for (int i = 0; i < strlen(s); i++)
```

### command-line arguments

argc: argument count

argv: argument vector (is an array of the arguments)

```c
#include <stdio.h>
int main(int argc, string argv[])
{
	printf("hello, %s\n", argv[1]);
}
```

and then in terminal:

```
make filename
./filename Lechi
hello, Lechi
```

注意：

1. 不是argv[0]
2. **argc是传递给应用程序的参数个数，argv是传递给应用程序的参数，且第一个参数为程序名。**

```c
#include <stdio.h>

int main(int argc, string argv[])
{
  if (argc == 2)
  {
    printf("hello, %s\n", argv[1]);
  }
  else
  {
    print("hello, world!");
  }
}
```

 **以上程序判断是否为一个输入参数时，argc需要和2比较**



### Exit status

Return non-zero value from main to exit from the program

Exp. return 1;

```c
#include <stdio.h>

int main(int argc, string argv[])
{
  if (argc != 2)
  {
    printf("sorry, something went wrong!");
    return 1;
  }
  else
  {
    print("hello, %s\n", argv[1]);
    return 0; 
  }
}
```

Error code 就是exit status

### functions

Function declarations

Return-type function-name(argument-list)

```c
// includes
#include <cs50.h>
#include <stdio.h>

// declare function prototype
int add_two_ints(int a, int b);

int main(void)
{
    // ask user for input
    int x = get_int("Give me an integer: ");
    int y = get_int("Give me another integer: ");

    // add the two numbers together via a function call
    int z = add_two_ints(x, y);

    // output the result
    printf("The sum of %i and %i is %i!\n", x, y, z);

}

int add_two_ints(int a, int b)
{
    int sum = a + b;
    return sum;
}
```

Valid_triangle

```c
bool valid_triangle(float a, float b, float c);

bool valid_triangle(float a, float b, float c)
{
  // check for all positive sides
  if (a <= 0 || b <= 0 || c <= 0)
  {
    return false;
  }
  // check that sum of any two sides greater than the third
  if ((a + b <= c) || (a + c <= b) || (b + C <= a))
  {
    return false;
  }
  // if the sides passed both two tests, then the triangle is valid
  return true;
}
```

### variable scope

local variable 

global variable

### compare string in C

use strcmp()

```c
if (strcmp(phrase, password) == 0)
```

### pass by value 

```c
#include <stdio.h>
#include <cs50.h>

int set_int(int x);

int main(void)
{
    int a = 5;
    a = set_int(a);
    printf("%i\n", a);
}

int set_int(int x)
{
    x = 20;
    return x;
}
```

输出的是20

```c
#include <stdio.h>
#include <cs50.h>

void set_int(int x);

int main(void)
{
    int a = 5;
    set_int(a);
    printf("%i\n", a);
}

void set_int(int x)
{
    x = 20;
}
```

输出时5

```c
#include <stdio.h>
#include <cs50.h>

void set_array(int x[4]);

int main(void)
{
    int number[4] = {1, 2, 3, 4};
    set_array(number);
    printf("%i\n", number[0]);
}

void set_array(int x[4])
{
    x[0] = 20;
}
```

输出为20，array时pass by reference，int是pass by value

### 两种不同的将字母转换成大写的方法

1. 只输出大写，但是不改变原来的字符串（有两种输出方式）

   ```c
   #include <ctype.h>
   #include <cs50.h>
   #include <stdio.h>
   #include <string.h>
   
   int main(void)
   {
       string s = get_string("Before: ");
     	int n = strlen(s);
       for (int i = 0; i < n; i++)
       {
       // 第一种输出方式
         printf("%c", toupper(s[i]));
       // 第二种输出方式
         putchar(toupper(s[i]));
       }
   }
   ```



2. 直接将整个字符串变成大写（也是两种操作方式）

   ```c
   #include <ctype.h>
   #include <cs50.h>
   #include <stdio.h>
   #include <string.h>
   
   int main(void)
   {
       string s = get_string("Before: ");
     	int n = strlen(s);
       for (int i = 0; i < n; i++)
       {
         // 直接使用ascii(这种方法的不足之处是需要使用for语句来避免非小写的情况，比如大写的E在这种情况下会变成%)
       	s[i] = s[i] - 32;
         // 调用toupper()
         s[i] = toupper(s[i]);
       }
     printf("%s", s);
   }
   ```

   

## WEEK 3 Algorithms

### searching

Focus on algorithms that solve problems with arrays

Efficiency - running time

Computer scientists tend to describe running time with **big O notation**, which we can think of as “on the order of” something, as though we want to convey an idea of running time and not an exact number of milliseconds or steps.

y = n x: Describe them both as having big O of n or on the order of n running time

y = lgx: it takes "big O of logn" steps (The base of the logarithm, 2, is also removed since it’s a constant factor.

common running times are as followed:
$$
O(n^2) \\
O(n\log_nn) \\
O(n) \\
O(log_nn) \\
O(1) \\
$$
Computer scientist also use big omega notation
$$
\omega
$$
Big Omega notation describes the lower bound of number of steps for our algorithm, or how few steps it might take, in  the best case. Big O, on the order of, is the upper bound of number of steps, or how many steps it might take, in the worst case.
$$
\omega(n^2) \\
\omega(n\log_nn) \\
\omega(n) \\
\omega(log_nn) \\
\omega(1) \\
$$
big Theta, which we use to describe running times of algorithms if the upper bound and lower bound is the same.
$$
\theta(n^2) \\
\theta(n\log_nn) \\
\theta(n) \\
\theta(log_nn) \\
\theta(1) \\
$$

if the running time is O(1), a constant of steps in a program is required no matter how big the problem is.

### linear search, binary search

Linear search: 从左到右一个个找

```pseudocode
For i from 0 to n-1
    If number behind doors[i]
        Return true
Return false
```

The big O running time is O(n)

the lower bound, big Omega would be omega(1)



If the numbers are sorted, we can use binary search

```pseudocode
If no doors
    Return false
If number behind doors[middle]
    Return true
Else if number < doors[middle]
    Search doors[0] through doors[middle - 1]
Else if number > doors[middle]
    Search doors [middle + 1] through doors[n - 1]
```

the big O running time is O(log n)

the lower bound, big Omega would be omega(1)

如果要用二分搜索的话，必须要先对数组进行排序



### searching with code

在c里面不能直接比较字符串是否相同，比如使用(name[1] == "Charlie")

但是可以使用`strcmp`来比较字符串

`strcmp` returns a negative value if the first string comes before the second string, `0` if the strings are the same, and a positive value if the first string comes after the second string.

如果第一个字符串在第二个字符串之前，' strcmp '返回负值，如果两个字符串相同，则返回' 0 '，如果第一个字符串在第二个字符串之后，则返回一个正值。

当字符串相同时返回找到：

```c
if (strcmp(names[i], "Ron") == 0)
        {
            printf("Found\n");
            return 0;
        }
```

或者

```c
if (!strcmp(names[i], "Ron"))
        {
            printf("Found\n");
            return 0;
        }
```



### structs (data structure)

a not well-designed way to maintain both names and their phone numbers in 2 arrays

```c
string names[] = {"Carter", "David"};
string numbers[] = {"+1-617-495-1000", "+1-949-468-2750"};
```

We can create a struct with a data type person that includes both names and phone numbers. define our own data structure with `typedef struct`

```c
typedef struct
{
  string name;
  string number;
}
person;
```

Exp. Phonebook

```c
#include <cs50.h>
#include <stdio.h>
#include <string.h>

typedef struct
{
    string name;
    string number;
}
person;

int main(void)
{
    person people[2];

    people[0].name = "Carter";
    people[0].number = "+1-617-495-1000";

    people[1].name = "David";
    people[1].number = "+1-949-468-2750";

    for (int i = 0; i < 2; i++)
    {
        if (strcmp(people[i].name, "David") == 0)
        {
            printf("Found %s\n", people[i].number);
            return 0;
        }
    }
    printf("Not found\n");
    return 1;
}
```

封装：encapulation is idea that related data is grouped together, and here we’ve encapsulated two pieces of information, `name` and `number` into the same data structure.



### sorting

Taking in an unsorted list of numbers as an imput and produce an output of a sorted list of numbers

#### selection sort demonstration

每次挑出list里最小的那个数然后和第一位的数进行交换

```pseudocode
For i from 0 to n–1
    Find smallest number between numbers[i] and numbers[n-1]
    Swap smallest number with numbers[i]
```

第一步是找出n个数里的最小值，第二步是n-1

所以总的是n+(n-1)+(n-2)+…(1)

计算为n(n+1)/2=n^2/2+n/2，当数据无限大时，upper bound of running time是O(n^2)

最小步骤的情况是整个list就是按照从小到大排列的，但是这个算法本身不会因为从小到大排列而自动退出，仍然会把所有过程走一遍，所以it has the lower bound of running time of \omega(n^2)



#### bubble sort demonstration

每次以相邻的连个数为单位，大小排序，然后一遍一遍排直到结束

需要注意的是，以52741630（一共8个数）为例，第一次两两比较排序后，最大值7必然会到达队尾；但是第二次操作操作仍然会对整个list操作一遍，包括最后一位的7

```pseudocode
Repeat n-1 times
    For i from 0 to n–2
        If numbers[i] and numbers[i+1] out of order
            Swap them
     If no waps
     Quit
```

一共需要n-1次，每次n-1次比较

一共是n^2-2n+1

upper bound of running time是O(n^2)

The lower bound 就是\omega(n)

#### recursion

就是function自己调用自己

原来的写方块

```
#
##
###
####
```

是这样

```c
#include <cs50.h>
#include <stdio.h>
  
void draw(int n);
  
int main(void)
{
    int height = get_int("Height: ");
  
    draw(height);
}
  
void draw(int n)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < i + 1; j++)
        {
            printf("#");
        }
        printf("\n");
    }
}
```

运用递归（将n层东西看成，n-1层加上n个#），自己调用自己（整个draw（）部分是从下往上写的）

```c
#include <cs50.h>
#include <stdio.h>

void draw(int n);

int main(void)
{
    int height = get_int("Height: ");

    draw(height);
}

void draw(int n)
{
    if (n <= 0)
    {
        return;
    }
    draw(n-1);
    for (int i = 0; i < n; i++)
    {
        printf("#");
    }
    printf("\n");
}
```

在比如阶乘：写一个factorial function来实现阶乘, 即：

fact(1)=1

Fact(2)=1*2

Fact(3)=1* 2 *3

Fact(n)=n*fact(n-1)

``` c
int fact(int n);
int fact(int n)
{
  // base case
  if (n == 1)
  {
    return 1;
  }
  //recursive case
 else
 {
   return n * fact(n-1);
 }
}
```

再再比如斐波那契数列：写个Fibonacci number sequence

```c
int fibo(int n);
int fibo(int n)
{
  if (n ==1)
    return 0;
 
  else if (n == 2)
    return 1;
  
  else
    return fibo(n-1) + fibo(n-2)
}
```

再比如：Collatz conjecture

![截屏2022-05-20 上午1.45.54](/Users/lechi/Library/Application Support/typora-user-images/截屏2022-05-20 上午1.45.54.png)

```c
int collatz(int n);
int collatz(int n)
{
  if (n == 1)
    return 0;
  
  else if ((n % 2) == 0)
    return collatz(n = n/2) + 1;
  
  else
    return collatz(3*n + 1) + 1;
  
}
```



#### merge sort

Merge sort是将递归思想运用在sort里

```pseudocode
If only one number
  Quit
Else
    Sort left half of number
    Sort right half of number
    Merge sorted halves
```

the upper bound of merge sort is O(nlogn)

the lower bound is also \omega(nlogn)

回忆cs50里八个数从最上面一层摆到最下面一层要经历3次下降（log2 8），每次下降这8个数每个都要比较然后放到下一层

所以是8log8，即n logn





## WEEK 4 

### pixels

- white, with R: 255, G: 255, and B: 255, and #FFFFFF
- red, with R: 255, G: 0, and B: 0, and #FF0000
- green, with R: 0, G: 255, and B: 0, and #00FF00
- blue, with R: 0, G: 0, and B: 255, and #0000FF
- black, #000000

### hexadecimal (十六进制)

```c
0 1 2 3 4 5 6 7 8 9 A B C D E F
```

helps us humans represent larger numeric values with fewer digits needed.



### addresses, pointers

- A **pointer** is a variable that stores an address in memory, where some other variable might be stored.

- The **`&`** operator can be used to get the address of some variable, as with `&n`. And the `*` operator declares a variable as a pointer, as with `int *p`, indicating that we have a variable called `p` that *points to* an `int`. So, to store the address of a variable `n` into a pointer `p`, we would write:

- &在告诉电脑这个值不是一个int而是某个变量的地址

  ```c
  int *p = &n;
  ```

```c
#include <stdio.h>

int main(void)
{
    int n = 50;
    int *p = &n;
    printf("%p\n", p);  // 0x7ffda0a4767c
    printf("%i\n", *p);  // 50
}

$ ./address
0x7ffda0a4767c
50
```

**segmentation faults**, where we’ve tried to read or write to memory we don’t have permission to.



### strings

We can declare a string with `string s = "HI!";`, which will be stored one character at a time in memory. And we can access each character with `s[0]`, `s[1]`, `s[2]`, and `s[3]`

s` is a variable of type `string`, which is a pointer to a character.

```c
#include <stdio.h>

int main(void)
{
    char *s = "HI!";
    printf("%s\n", s);
}
```

to see the addresses of characters in a string

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string s = "HI!";
    char *p = &s[0];
    printf("%p\n", p);
    printf("%p\n", s);
}
```

### pointer arithmetic

```c
#include <stdio.h>

int main(void)
{
    char *s = "Hi!";
    printf("%c\n", *s);
    printf("%c\n", *（s + 1）);
    printf("%c\n", *（s + 2）);
    
    // 或者等效以下
    char *s = "HI!";
    printf("%c\n", s[0]);
    printf("%c\n", s[1]);
    printf("%c\n", s[2]);
}
```

`*s` goes to the address stored in `s`, and `*(s + 1)` goes to the location in memory with the next character, an address that is one byte higher.

`s[1]` is **syntactic sugar**, like an abstraction for `*(s + 1)`, equivalent in function but more human-friendly to read and write.

### pointers

pointers provide an alternative way to pass data between functions

- when we pass data by value, we only pass a copy of that data

if we use pointers instead, we have power to pass the actual variable itself

| data type | size |
| --------- | ---- |
| int       | 4    |
| char      | 1    |
| float     | 4    |
| double    | 8    |
| long long | 8    |
| string    | ?    |

& is used to extract the exact address of an already existing variable

array的名称本身就是pointer  

segmentation fault: go to the NULL place 

dereferenfce: int* p 就是去到p的地址，然后找到对应的p值

if i want to identify multiple pointers in one line, we can use 

```
int* pa, *pb, *pc;
```



### compare and copy

```c
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    char *s = get_string("s: ");
    char *t = get_string("t: ");

    if (s == t)
    {
        printf("Same\n");
    }
    else
    {
        printf("Different\n");
    }
}


$ make compare
$ ./compare
s: HI!
t: BYE!
Different
$ ./compare
s: HI!
t: HI!
Different
```

- Even when our inputs are the same, we see “Different” printed.
- Each “string” is a pointer, `char *`, to a different location in memory, where the first character of each string is stored. So even if the characters in the string are the same, this will always print “Different”.

### memory allocation

- We’ll need to use a new function, `malloc`, to allocate some number of bytes in memory. And we’ll use `free` to mark memory as usable when we’re done with it, so the operating system can do something else with it.
  - Our computers might slow down if a program we’re running has a bug where it allocates more and more memory but never frees it. The operating system will take longer and longer to find enough available memory for our program.

```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
    char *s = get_string("s: ");

    char *t = malloc(strlen(s) + 1);

    for (int i = 0, n = strlen(s) + 1; i < n; i++)
    {
        t[i] = s[i];
    }

    t[0] = toupper(t[0]);

    printf("s: %s\n", s);
    printf("t: %s\n", t);
}
```

快捷字符串替换

```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
    char *s = get_string("s: ");

    char *t = malloc(strlen(s) + 1);

    strcpy(t, s);

    t[0] = toupper(t[0]);

    printf("s: %s\n", s);
    printf("t: %s\n", t);

    free(t);
}
```

We can add some error-checking to our program:

```c
#include <cs50.h>
#include <ctype.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main(void)
{
    char *s = get_string("s: ");

    char *t = malloc(strlen(s) + 1);
    if (t == NULL)
    {
        return 1;
    }

    strcpy(t, s);

    if (strlen(t) > 0)
    {
        t[0] = toupper(t[0]);
    }

    printf("s: %s\n", s);
    printf("t: %s\n", t);

    free(t);
}
```

- If our computer is out of memory, `malloc` will return `NULL`, the null pointer, or a special value of all `0` bits that indicates there isn’t an address to point to. So we should check for that case, and exit if `t` is `NULL`.
- We should also check that `t` has a length, before trying to capitalize the first character.

### valgrind 内存泄露

- **`valgrind`** is a command-line tool that we can use to run our program and see if it has any memory-related issues.
- We’ll run `valgrind ./filename` after compiling, and we’ll see a lot of output

```c
int *x = malloc(3 * sizeof(int));
```





#### garbage values

```c
int main(void)
{   
    int *x;  
    int *y; 

    x = malloc(sizeof(int));                    

    *x = 42;
    *y = 13;    

    y = x;        

    *y = 13;   
}
```

- In the first two lines, we declare two pointers. Then, we allocate memory for `x`, but not `y`, so we can assign a value to the memory `x` is pointing to with `*x = 42;`. But `*y = 13;` is problematic, since we haven’t allocated any memory for `y`, and the garbage value there points to some area in memory we likely don’t have access to.
- We can write `y = x;` so that `y` points to the same allocated memory as `x`, and use `*y = 13;` to set the value there.

### define custom types

typedef <old name> <new name>;

```c
struct car
{
	int year;
    char model[10];
    char plate[7];
    int odometer;
    double engine_size;
    
}

typedef struct car car_t;

or we can use:

typedef struct car
{
    int year;
    char model[10];
    char plate[7];
    int odometer;
    double engine_size;
}
car_t;
```

### dynamic memory allocation

text

initialized data

uninitialized data

heap

stack

environment variables



statically obtain an integer

int x;

dynamically obtain an intetger

int *px = malloc(sizeof(int));

```c
// get an integer from the user
int x = GetInt();
// array of floats on the stack
float stack_array[x];
// array of floats on the heap
float* heap_array = malloc(x * sizeof (float));
```



### free memory

every block of memory that you malloc(), should be free()

### swap

```c
void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```

```c
#include <stdio.h>

void swap(int *a, int *b);

int main(void)
{
    int x = 1;
    int y = 2;

    printf("x is %i, y is %i\n", x, y);
    swap(&x, &y);
    printf("x is %i, y is %i\n", x, y);
}

void swap(int *a, int *b)
{
    int tmp = *a;
    *a = *b;
    *b = tmp;
}
```

With `&x`, we can get the address of `x` to pass in.

- The **machine code** section is our compiled program’s binary code. When we run our program, that code is loaded into memory.
- Just below, or in the next part of memory, are **global variables** we declared in our program.
- The **heap** section is an empty area from where `malloc` can get free memory for our program to use. As we call `malloc`, we start allocating memory from the top down.
- The **stack** section is used by functions and local variables in our program as they are called, and grows upwards.
- 
  If we call `malloc` for too much memory, we will have a **heap overflow**, since we end up going past our heap. Or, if we call too many functions without returning from them, we will have a **stack overflow**, where our stack has too much memory allocated as well.

### scnaf

```c
#include <stdio.h>

int main(void)
{
    int x;
    printf("x: ");
    scanf("%i", &x);
    printf("x: %i\n", x);
}
```

```c
#include <stdio.h>

int main(void)
{
    char *s;
    printf("s: ");
    scanf("%s", s);
    printf("s: %s\n", s);
}
```


We can call `malloc` to allocate memory:

```c
#include <stdio.h>

int main(void)
{
    char *s = malloc(4);
    printf("s: ");
    scanf("%s", s);
    printf("s: %s\n", s);
}
```





### files

```c
// Saves names and numbers to a CSV file
  
#include <cs50.h>
#include <stdio.h>
#include <string.h>
  
int main(void)
{
    // Open CSV file
    FILE *file = fopen("phonebook.csv", "a");
    if (!file)
    {
        return 1;
    }
  
    // Get name and number
    string name = get_string("Name: ");
    string number = get_string("Number: ");
  
    // Print to file
    fprintf(file, "%s,%s\n", name, number);
  
    // Close file
    fclose(file);
}
```

- `fopen` is a new function we can use to open a file with a new type, `FILE`.
- We can use `fprintf` to write to a file.

the file manipulation functions all live in stdio.h

fopen() FILE* ptr = fopen(<filename>, <operation>);

FILE* ptr1 = fopen(<feile3.txt>, <r>);

read append



fclose()

fclose(ptr1)



fgetc() file get a character

char ch = fgetc(<file.txt>)

read all the characters fron a file:

```c
char ch;
while ((ch = fgetc(ptr)) != EOF);
printf("%c", ch);
```

EOF end of file



fputc()



fread()

fread(<buffer>, <size>, <qty>, <file pointer>); 

```c
int arr[10];
fread(arr, sizeof(int), 10, ptr);

double* arr2 = malloc(sizeof(double) * 80);
fread(arr2, sizeof(double), 80, ptr);

char c;
fread(&c, sizeof(char), 1, ptr); // 第一个空必须指向一个地址(pointed by <buffer>)
```



fwrite()

fwrite(<buffer>, <size>, <qty>, <file pointer>); 

```c
int arr[10];

fwrite(arr, sizeof(int), 10, ptr);
```





### jpeg

Let’s look at a program that opens a file and tells us if it’s a JPEG file, a particular format for image files, with [`jpeg.c`](https://cdn.cs50.net/2021/fall/lectures/4/src4/jpeg.c?highlight):

```c
// Detects if a file is a JPEG
  
#include <stdint.h>
#include <stdio.h>
  
typedef uint8_t BYTE;
  
int main(int argc, char *argv[])
{
    // Check usage
    if (argc != 2)
    {
        return 1;
    }
  
    // Open file
    FILE *file = fopen(argv[1], "r");
    if (!file)
    {
        return 1;
    }
  
    // Read first three bytes
    BYTE bytes[3];
    fread(bytes, sizeof(BYTE), 3, file);
  
    // Check first three bytes
    if (bytes[0] == 0xff && bytes[1] == 0xd8 && bytes[2] == 0xff)
    {
        printf("Yes, possibly\n");
    }
    else
    {
        printf("No\n");
    }
  
    // Close file
    fclose(file);
}



$ make jpeg
$ ./jpeg .src4/lecture.jpg
Yes, possibly
```


We’ll learn more about these in this week’s problem set as well, and even implement our own version of image filters, like one that only shows the color red:

```c
#include "helpers.h"
  
// Only let red through
void filter(int height, int width, RGBTRIPLE image[height][width])
{
    // Loop over all pixels
    for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width; j++)
        {
            image[i][j].rgbtBlue = 0x00;
            image[i][j].rgbtGreen = 0x00;
        }
    }
}

make filter
./filter hidden.bmp newfilename.bmp
code newfilename.bmp
    
```





## WEEK 5

### linked lists 链表

```c
typedef struct node
{
    int number;
    struct node *next;
}
node;

node *list = NULL;
node *n = malloc(sizeof(node));

if (n != NULL)
{
  (*n).number = 1;
}

if (n != NULL)
{
    n->number = 1;
    n->next = NULL;
}

list = n; 

```

- We start this struct with `typedef struct node` so that we can refer to a `struct node` inside our struct.
- Then, we’ll have an `int` called `number`, for the value we want to store, and then a pointer to the next node with `struct node`. (We haven’t fully defined `node` yet, so the compiler needs to know it’s a custom struct still.)
- Finally, `node` at the end lets us use just `node` in the rest of our program.

### grwoing arrays

```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *list = malloc(3 * sizeof(int));
    if (list == NULL)
    {
        return 1;
    }
    
    list[0] = 1;
    list[1] = 2;
    list[2] = 3;
}
```

`if (list = NULL)` 这句是为了防止在memory allocation的时候产生错误没有成功为list 产生空间，因为malloc功能会fail

这个方法和以下代码的区别是这个是从heap中的memory来产生这个list的

```c
int list[3];
list[0] = 1;
list[1] = 2;
list[2] = 3;
```


```c
#include <stdio.h>
#include <stdlib.h>

int main(void)
{
    int *list = malloc(3 * sizeof(int));
    if (list == NULL)
    {
        return 1;
    }
    
    list[0] = 1;
    list[1] = 2;
    list[2] = 3;
    
    int *temp = malloc(4 * sizeof(int));
    if (temp == NULL)
    {
        free(list);
        return 1;
    }
    
    for (int i = 0; i < 3; i++)
    {
        temp[i] = list[i];
    }
    temp[3] = 4;
    
    free(list);
    list = temp;
    for (int i = 0; i < 4; i++)
    {
        printf("%i\n", list[i]);
    }
    free(list);
    return 0;
    
    
    
}
```

use `realloc` resize old aaray to be certain size

```c
#include <stdio.h>
#include <stdlib.h>
  
int main(void)
{ 
    // Dynamically allocate an array of size 3
    int *list = malloc(3 * sizeof(int));
    if (list == NULL)
    {
        return 1;
    }
  
    // Assign three numbers to that array
    list[0] = 1;
    list[1] = 2;
    list[2] = 3;

    // Time passes

    // Resize old array to be of size 4
    int *tmp = realloc(list, 4 * sizeof(int));
    if (tmp == NULL)
    {
        free(list);
        return 1;
    }

    // Add fourth number to new array
    tmp[3] = 4;

    // Remember new array
    list = tmp;

    // Print new array
    for (int i = 0; i < 4; i++)
    {
        printf("%i\n", list[i]);
    }

    // Free new array
    free(list);
    return 0;
}
```



### growing linked lists

```c
typedef struct node
{
    int number;
    struct node *next;
}
node;

node *list = NULL;
node *n = malloc(sizeof(node));

if (n != NULL)
{
  (*n).number = 1;
}

if (n != NULL)
{
    n->number = 1;
    n->next = NULL;
}

list = n; 


n = malloc(sizeof(node));
if (n != NULL)
{
    n->number = 2;
    n->next = NULL;
}
list->next = n;

node *n = malloc(sizeof(node));
if (n != NULL)
{
    n->number = 3;
    n->next = NULL;
}

list->next->next = n;

```



### implementing linked lists

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;
    struct node *next;
}
node;

int main(void)
{
    node *list = NULL;
    node *n = malloc(sizeof(node));
    if (n == NULL)
    {
        return 1;
    }
    n->number = 1;
    n->next = NULL;
    list = n;
    
    n = malloc(sizeof(node));
    if (n == NULL)
    {
        free(list);
        return 1;
    }
    n->number = 2;
    n->next = NULL;
    list->next = n;
    
    n = malloc(sizeof(node));
    if(n == NULL)
    {
        free(list->next);
        free(list);
        return 1;
    }
    n->number = 3;
    n->next = NULL;
    list->next->next = n;
    
    for (node *temp = list; temp != NULL; temp = temp->next)
    {
        printf("%i", temp->number);
    }
    while (list != NULL)
    {
        node *temp = list->next;
        free(list);
        list = tmp;
    }
    return 0;
    
    
}

```

### trees

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int number;
    struct node *left;
    struct node *right;
    
}
node;

int main(void)
{
    // set the tree size to 0
    node *tree = NULL;
    
    // add number to list
    node *n = malloc(sizeof(node));
    if(n == NULL)
    {
        return 1;
    }
    n->number = 2;
    n->left = NULL;
    n->right = NULL;
    tree = n;
    
    n = malloc(sizeof(node));
    if(n == NULL)
    {
        free_tree(tree);
        return 1;
       
    }
    n->number = 1;
    n->left = NULL;
    n->right = NULL;
    tree->left = n;
    
    n = malloc(sizeof(node));
    if(n == NULL)
    {
        free_tree(tree);
        return 1;
       
    }
    n->number = 3;
    n->left = NULL;
    n->right = NULL;
    tree->right = n;
    
    print_tree(tree);
    return 0;
    
}


```



### more data structres

















