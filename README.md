# hossam
import time
import pandas as pd
import numpy as np

CITY_DATA = {'chicago': 'chicago.csv',
              'new york city': 'new_york_city.csv',
              'washington': 'washington.csv'}

def check_input(input_str,input_type):
    """
    check the validity of user input.
    input_str: is the input of the user
    input_type: is the type of input: 1 = city, 2 = month, 3 = day
    """
    while True:
        input_read=input(input_str)
        try:
            if input_read in ['chicago','new york city','washington'] and input_type == 1:
                break
            elif input_read in ['january', 'february', 'march', 'april', 'may', 'june','all'] and input_type == 2:
                break
            elif input_read in ['sunday','monday','tuesday','wednesday','thursday','friday','saturday','all'] and input_type == 3:
                break
            else:
                if input_type == 1:
                    print("Sorry, your input should be: chicago new york city or washington")
                if input_type == 2:
                    print("Sorry, your input should be: january, february, march, april, may, june or all")
                if input_type == 3:
                    print("Sorry, your input should be: sunday, ... friday, saturday or all")
        except ValueError:
            print("Sorry, your input is wrong")
    return input_read

def get_filters():
    """
    Asks user to specify a city, month, and day to analyze.
    Returns:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    """
    print('Hello! Let\'s explore some US bikeshare data!')
    # get user input for city (chicago, new york city, washington). HINT: Use a while loop to handle invalid inputs
    city = check_input("Would you like to see the data for chicago, new york city or washington?",1)
    # get user input for month (all, january, february, ... , june)
    month = check_input("Which Month (all, january, ... june)?", 2)
    # get user input for day of week (all, monday, tuesday, ... sunday)
    day = check_input("Which day? (all, monday, tuesday, ... sunday)", 3)
    print('-'*40)
    return city, month, day

raw = {'chicago': 'chicago.csv','new york city': 'new_york_city.csv', 'washington': 'washington.csv'}

def get_from_files(city, month, day):
    df = pd.read_csv(raw[city])
def load_data(city, month, day):
    """
    Loads data for the specified city and filters by month and day if applicable.
    Args:
        (str) city - name of the city to analyze
        (str) month - name of the month to filter by, or "all" to apply no month filter
        (str) day - name of the day of week to filter by, or "all" to apply no day filter
    Returns:
        df - Pandas DataFrame containing city data filtered by month and day
    """
    # load data file into a dataframe
    df = pd.read_csv(CITY_DATA[city])

    # convert the Start Time column to datetime
    df['Start Time'] = pd.to_datetime(df['Start Time'])

    # extract month, day of week, hour from Start Time to create new columns
    df['month'] = df['Start Time'].dt.month
    df['day_of_week'] = df['Start Time'].dt.weekday_name
    df['hour'] = df['Start Time'].dt.hour
@@ -25,73 +89,62 @@ def get_from_files(city, month, day):

    return df

def choices():
    city = test_string("Choose a City chicago, new york city or washington?", 'a')
    month = test_string("Choose a month  january, ... june or all", 'b')
    day = test_string("Choose a day monday, tuesday, ... sunday or all", 'c')
    return city, month, day

def test_string(user_str,type):
    #The user can retry one hadered times until correct
    for x in range(100):
        result_str=input(user_str).lower()
        try:
            if type == 'a' and result_str in ['chicago','new york city','washington']:
                break
            elif type == 'b' and result_str in ['all','january', 'february', 'march', 'april', 'may', 'june']:
                break
            elif type == 'c' and result_str in ['all','sunday','monday','tuesday','wednesday','thursday','friday','saturday']:
                break
            else:
                if type == 'a':
                    print("Valid: chicago new york city or washington")
                if type == 'b':
                    print("Valid: january, february, march, april, may, june or all")
                if type == 'c':
                    print("Valid: sunday, ... friday, saturday or all")
        except ValueError:
            print("Sorry, your input is wrong")
    return result_str



def time_stats(df):
    """Displays statistics on the most frequent times of travel."""

def get_stats(df,city):
    print('\nCalculating The Most Frequent Times of Travel...\n')
    start_time = time.time()

    # display the most common month
    most_common_month = df['month'].mode()[0]
    popular_month = df['month'].mode()[0]

    print('Most Popular Month:', most_common_month)
    print('Most Popular Month:', popular_month)

    # display the most common day of week
    most_common_day_of_week = df['day_of_week'].mode()[0]
    popular_day_of_week = df['day_of_week'].mode()[0]

    print('Most Day Of Week:',  most_common_day_of_week)
    print('Most Day Of Week:', popular_day_of_week)

    # display the most common start hour
    most_common_start_hour = df['hour'].mode()[0]
    popular_common_start_hour = df['hour'].mode()[0]

    print('Most Common Start Hour:', popular_common_start_hour)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


    print('Most Common Start Hour:',  most_common_start_hour)
def station_stats(df):
    """Displays statistics on the most popular stations and trip."""

    print('\nCalculating The Most Popular Stations and Trip...\n')
    start_time = time.time()

    # display most commonly used start station
    most_common_start_station = df['Start Station'].mode()[0]
    popular_start_station = df['Start Station'].mode()[0]

    print('Most Start Station:', most_common_start_station)
    print('Most Start Station:', popular_start_station)

    # display most commonly used end station
    most_common_end_station = df['End Station'].mode()[0]
    popular_end_station = df['End Station'].mode()[0]

    print('Most End Station:',  most_common_end_station)
    print('Most End Station:', popular_end_station)

    # display most frequent combination of start station and end station trip
    group_of_start_end = df.groupby(['Start Station', 'End Station'])
    most_common_combination_station = group_of_start_end.size().sort_values(ascending=False).head(1)
    print('Most frequent combination of Start Station and End Station trip:\n', most_common_combination_station)
    group_field=df.groupby(['Start Station','End Station'])
    popular_combination_station = group_field.size().sort_values(ascending=False).head(1)
    print('Most frequent combination of Start Station and End Station trip:\n', popular_combination_station)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def trip_duration_stats(df):
    """Displays statistics on the total and average trip duration."""

    print('\nCalculating Trip Duration...\n')
    start_time = time.time()

    # display total travel time
    total_travel_time = df['Trip Duration'].sum()
@@ -103,7 +156,16 @@ def get_stats(df,city):

    print('Mean Travel Time:', mean_travel_time)

    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def user_stats(df,city):
    """Displays statistics on bikeshare users."""

    print('\nCalculating User Stats...\n')
    start_time = time.time()

    # Display counts of user types
    print('User Type Stats:')
    print(df['User Type'].value_counts())
@@ -114,33 +176,29 @@ def get_stats(df,city):
        # Display earliest, most recent, and most common year of birth
        print('Birth Year Stats:')
        most_common_year = df['Birth Year'].mode()[0]
        print('Most Common Year:', most_common_year)
        print('Most Common Year:',most_common_year)
        most_recent_year = df['Birth Year'].max()
        print('Most Recent Year:', most_recent_year)
        print('Most Recent Year:',most_recent_year)
        earliest_year = df['Birth Year'].min()
        print('Earliest Year:', earliest_year)
        print('Earliest Year:',earliest_year)
    print("\nThis took %s seconds." % (time.time() - start_time))
    print('-'*40)


def main():
    pd.set_option('display.max_columns', None)
    # The user can replay the program 100 times
    for x in range(100):
        city, month, day = choices()
        df = get_from_files(city, month, day)

        get_stats(df,city)
        rows=0;
        # The user can replay this option 100 times
        for x in range(100):
            print(df[rows:rows + 5])
            more_rows = input('\nMore individual trips? (yes/no).\n')
            rows=rows+5
            if more_rows.lower() != 'yes':
                break
        restart = input('\nRestart? (yes/no).\n')
    while True:
        city, month, day = get_filters()
        df = load_data(city, month, day)

        time_stats(df)
        station_stats(df)
        trip_duration_stats(df)
        user_stats(df,city)

        restart = input('\nWould you like to restart? Enter yes or no.\n')
        if restart.lower() != 'yes':
            break


if __name__ == "__main__":
	main()
