# DATACLEANING-NASHVILLEHOUSING
These scripts collectively serve as a comprehensive data cleaning and transformation process applied to the Nashville_Housing table

Here's a summarized overview:
1. Viewing Data:
   - Retrieves all records and specific columns for inspection.
2. Date Standardization:
   - Converts `SaleDate` to a proper DATE format and adds a new column `SaleDateConverted` with the same converted date.
3. Address Data Population: 
   - Fills `PropertyAddress` where it's NULL by joining with other records sharing the same `ParcelID`.
4. Address Parsing:
   - Breaks `PropertyAddress` into separate `Address` and `City` components using `SUBSTRING` and `CHARINDEX`.
   - Adds new columns `PropertySplitAddress` and `PropertySplitCity` and updates them accordingly.
   - Alternative method for splitting addresses using `PARSENAME` after replacing commas with periods.
5. Owner Address Parsing: 
   -Similar approach to split `OwnerAddress` into `OwnerSplitAddress`, `OwnerSplitCity`, and `OwnerSplitState`.
6. Data Type Conversion & Recoding:
   - Changes `SoldAsVacant` from `BIT` to `CHAR(3)` through adding a new column `SoldAsNewVacant`.
   - Populates the new column based on the original bit values.
   - Converts numeric values to 'YES'/'NO'` strings.
7. Removing Duplicates: 
   - Uses a Common Table Expression (CTE) with `ROW_NUMBER()` to identify duplicates based on multiple columns, with a suggestion to delete duplicates.
8. Clean-up:
   - Drops unused or raw data columns like `PropertyAddress`, `SaleDate`, `OwnerAddress`, `TaxDistrict`, and `SoldAsVacant`.
---

### RECOMMENDATIONS:

i. Backup Data: 
   - Before dropping columns or deleting records, ensure you have a backup.

ii. Consistent Address Parsing: 
   - Use a single, robust method for splitting addresses—`PARSENAME` can be limited if addresses do not follow the expected format.

iii. Data Type Handling: 
   - Instead of adding new columns for conversion, consider altering existing columns if appropriate.

iv. Duplicate Removal: 
   - Be cautious when deleting duplicates; review the criteria thoroughly.

v. Code Optimization: 
   - Avoid redundant steps, for example, multiple methods for splitting addresses. Choose the most reliable one.

vi. Validation: 
   - After transformations, run validation queries to ensure data integrity.
---
