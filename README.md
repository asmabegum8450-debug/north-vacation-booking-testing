partner :Ermiyas Hailemichael
# North Vacation Booking — Black-Box Testing, Part 1

## Overview

This project uses black-box testing and equivalence partitioning to design test cases for the North Vacation Booking application without accessing its source code.

## Equivalence Partition Tables

### 1. Number of Nights

| Partition | Range or Condition | Representative Input | Expected Result |
|---|---|---|---|
| Invalid low | 0 or fewer nights | 0 | ValueError |
| Valid | 1–31 nights | 7 | Reservation accepted |
| Invalid high | More than 31 nights | 32 | ValueError |

### 2. Number of Guests

| Partition | Range or Condition | Representative Input | Expected Result |
|---|---|---|---|
| Invalid low | Fewer than 1 guest | 0 | ValueError |
| Valid standard | 1–5 guests | 3 | No extra guest fee |
| Valid additional fee | 6–12 guests | 7 | $25 per additional guest per night |
| Invalid high | More than 12 guests | 13 | ValueError |

### 3. Check-in and Checkout Dates

| Partition | Condition | Representative Input | Expected Result |
|---|---|---|---|
| Valid | Check-in before checkout, 1–31 nights | Oct 10–Oct 13 | 3 nights |
| Invalid same day | Check-in equals checkout | Oct 10–Oct 10 | ValueError |
| Invalid reversed | Check-in after checkout | Oct 13–Oct 10 | ValueError |

### 4. Availability

| Partition | Condition | Representative Input | Expected Result |
|---|---|---|---|
| Valid | All requested nights available | 3 available nights | Reservation accepted |
| Invalid | At least one requested night unavailable | 1 unavailable night | UnavailableError |

## Test Cases

All valid test cases assume that the requested nights are available unless stated otherwise.

| ID | Classification | Partition | Input | Expected Result |
|---|---|---|---|---|
| TC01 | Nights | Invalid low | 0 nights, 3 guests | ValueError |
| TC02 | Nights | Valid | 7 nights, 3 guests | Accepted; total $1,450 |
| TC03 | Nights | Invalid high | 32 nights, 3 guests | ValueError |
| TC04 | Guests | Invalid low | 3 nights, 0 guests | ValueError |
| TC05 | Guests | Valid standard | 3 nights, 3 guests | Accepted; total $650 |
| TC06 | Guests | Valid additional fee | 3 nights, 7 guests | Accepted; total $800 |
| TC07 | Guests | Invalid high | 3 nights, 13 guests | ValueError |
| TC08 | Dates | Valid | Oct 10–Oct 13, 3 guests | Accepted; 3 nights; total $650 |
| TC09 | Dates | Invalid same day | Oct 10–Oct 10, 3 guests | ValueError |
| TC10 | Dates | Invalid reversed | Oct 13–Oct 10, 3 guests | ValueError |
| TC11 | Availability | Valid | Oct 10–Oct 13, all nights available | Accepted |
| TC12 | Availability | Invalid | Oct 10–Oct 13, Oct 11 unavailable | UnavailableError |

## Pricing Formula

Total = (Nights × $200) + $50 + (Nights × $25 × max(0, Guests - 5))

The cleaning fee is charged once for each valid reservation.

The checkout date is not counted as a reserved night.

## Why Equivalence Partitioning?

Equivalence partitioning reduces the number of test cases by grouping inputs that should produce similar results. Instead of testing every possible number of nights or guests, representative values are selected from valid and invalid partitions.

## AI Transparency

ChatGPT was used to help organize the equivalence partition tables, calculate expected prices, and draft test cases. The test cases were designed from the provided requirements without accessing application source code.

## Reference

GeeksforGeeks. (2026, July 3). *Equivalence partitioning method*. https://www.geeksforgeeks.org/software-engineering/equivalence-partitioning-method/
