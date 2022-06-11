Functional decomposition means breaking it down into a number of discrete steps that the process performs.

For example, making a cup of tea might involve:

- Getting a cup
- Putting teabag in cup
- Put water in kettle
- Boil water
- Add water to the teabag-filled cup


        function giveBonus(currentYear, price) {
        if ((currentYear % 2 === 0) && price > SUPER_THRESHOLD) {
            return SUPER_BONUS;
        }
        return price > BASIC_THRESHOLD ? NORMAL_BONUS : 0;
        }
    
    --------------------------------------------------------
    
        function giveBonus(currentYear, price) {
        if (isLeapYear(currentYear) && 
                priceQualifiesForSuperBonus(price)) {
            return SUPER_BONUS;
        }
        if (qualifiesForNormalBonus(price)) {
            return NORMAL_BONUS;
        }
        return 0;
        }
