# Shopify Fall 2022 Data Science Intern Challenge (Part 2)

Please consider donating to the **Palestine Emergency Appeal**. The smallest of contributions can make the most profound of impacts.

<a href="https://www.islamicreliefcanada.org/emergencies/palestine/" target="_blank" rel="noopener noreferrer" style="color: white; background-color: salmon; border-radius: 5px; padding: 5px;">Donate to Palestine</a>

## Challenge

For this question you’ll need to use SQL. [Follow this link](https://www.w3schools.com/SQL/TRYSQL.ASP?FILENAME=TRYSQL_SELECT_ALL) to access the data set required for the challenge. Please use queries to answer the following questions. Paste your queries along with your final numerical answers below.

- How many orders were shipped by Speedy Express in total?
- What is the last name of the employee with the most orders?
- What product was ordered the most by customers in Germany?

## How many orders were shipped by Speedy Express in total?

```sql
SELECT COUNT(*) AS SpeedyExpressOrdersCount
FROM Orders WHERE ShipperID = (
    SELECT ShipperID
    FROM Shippers WHERE ShipperName = 'Speedy Express'
);
```

<table>
<tr>
<th>
SpeedyExpressOrdersCount
</th>
</tr>
<tr>
<td>
54
</td>
</tr>
</table>

## What is the last name of the employee with the most orders?

```sql
SELECT COUNT(O.EmployeeID) AS EmployeeOrdersCount, FirstName, LastName
FROM Orders AS O INNER JOIN Employees AS E
ON O.EmployeeID = E.EmployeeID
GROUP BY O.EmployeeID
ORDER BY EmployeeOrdersCount DESC
LIMIT 1;
```

<table>
<tr>
<th>
EmployeeOrdersCount
</th>
<th>
FirstName
</th>
<th>
LastName
</th>
</tr>
<tr>
<td>
40
</td>
<td>
Margaret
</td>
<td>
Peacock
</td>
</tr>
</table>

## What product was ordered the most by customers in Germany?

```sql
SELECT P.ProductName, SUM(Quantity) AS TotalQuantity FROM OrderDetails AS OD
INNER JOIN Orders AS O ON O.OrderID = OD.OrderID
INNER JOIN Customers AS C ON C.CustomerID = O.CustomerID
INNER JOIN Products AS P ON P.ProductID = OD.ProductID
WHERE Country = 'Germany'
GROUP BY P.ProductID
ORDER BY TotalQuantity
LIMIT 1;
```

<table>
<tr>
<th>
ProductName
</th>
<th>
TotalQuantity
</th>
</tr>
<tr>
<td>
NuNuCa Nuß-Nougat-Creme
</td>
<td>
4
</td>
</tr>
</table>
