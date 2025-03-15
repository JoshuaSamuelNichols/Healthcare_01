# **Healthcare Querying with SQL**


<img src="https://github.com/user-attachments/assets/3bd5e564-e907-4dac-a2b5-eee914f744c7" width="300" />

## **Introduction**
Healthcare organizations generate massive amounts of data daily. Hospitals, clinics, and insurance providers rely on data analysts to extract insights that improve patient outcomes, optimize resources, and reduce costs. SQL is the backbone of healthcare analytics, allowing professionals to query and analyze structured data efficiently.

This project uses [generalized data](https://drive.proton.me/urls/Q1PPWEXSX4#FYEOZO2MQvRR) for analysts to work with using SQL to derive insights from **appointments**, **billing records**, **prescribed medications**, and **patient demographics**.

I am using [Visual Studio Code](https://code.visualstudio.com/) which was a bit of work to fix up with SQLite but you can get by much easier using the [SQLite App](https://sqlitebrowser.org/). Don't forget to check out the DataCamp details at the end for more Data Science!

---

## **Understanding Your Data Landscape**
Before writing queries, analysts start by understanding the data. This dataset contains:

| Table Name     | Description |
|---------------|-------------|
| **patients**  | Contains patient demographic details such as name, age, gender, and insurance provider. |
| **appointments** | Tracks patient appointments, including date, doctor, and appointment status. |
| **billing**   | Contains medical billing records, including amount due and amount paid. |
| **medications** | Lists prescribed medications, their dosage, and the associated patient. |

To get an overview of the dataset:
```sql
SELECT * FROM patients LIMIT 10;
```



![image](https://github.com/user-attachments/assets/51d48233-09c1-4b3a-abf0-c8868bb85e8c)


---

## **Uncovering Key Trends in Patient Appointments**
Hospital administrators track patient volume across departments to allocate resources efficiently.
```sql
SELECT doctor, COUNT(appointment_ID) AS appointment_count
FROM appointments
GROUP BY doctor
ORDER BY appointment_count DESC;
```
![image](https://github.com/user-attachments/assets/0953e0bd-f143-43b3-b159-b1fed20dba2b)


**Key Insight:** Identifies which doctors handle the most appointments, helping with workload balancing.

---

## **Identifying Outstanding Medical Bills**
Unpaid medical bills impact hospital finances. Analyzing billing data helps track overdue payments.
```sql
SELECT customer_ID, amount_due, amount_paid
FROM billing
WHERE amount_due > amount_paid
LIMIT 20;
```

![image](https://github.com/user-attachments/assets/43c5f101-2e5d-44af-957e-1376920605f5)


**Key Insight:** Identifies patients with outstanding balances, aiding in financial planning.

---

## **Mapping Insurance Coverage Gaps**
Understanding the proportion of insured versus uninsured patients helps in policy-making and financial aid planning.
```sql
SELECT insurance_provider, COUNT(customer_ID) AS patient_count
FROM patients
GROUP BY insurance_provider;
```

![image](https://github.com/user-attachments/assets/2d9e2bc7-f708-4f7d-b4c9-7a649b2420c3)

**Key Insight:** Determines the percentage of uninsured patients and the hospital’s financial risk exposure.

---

## **Forecasting Patient Demand Over Time**
Analyzing visit trends helps predict patient demand and optimize hospital operations.
```sql
SELECT strftime('%Y-%m', date) AS month, COUNT(appointment_ID) AS patient_count
FROM appointments
GROUP BY month
ORDER BY month;
```
![image](https://github.com/user-attachments/assets/700e083d-bd7d-41f9-abe6-efbf689bc4c0)


**Key Insight:** Identifies seasonal trends in patient visits to adjust staffing and resource allocation.

---

## **Detecting Anomalies in Medical Billing**
Unusual patterns in healthcare claims could indicate fraud or billing errors.
```sql
SELECT customer_ID, SUM(amount_due) AS total_billed
FROM billing
GROUP BY customer_ID
HAVING total_billed > (SELECT AVG(amount_due) * 3 FROM billing);
```

![image](https://github.com/user-attachments/assets/c1add86d-75ff-4a18-9a02-b91e0f79175b)


**Key Insight:** Identifies patients with excessive billing that may require audit.

---

## **Optimizing Costs with Smarter Treatment Choices**
Comparing different medications prescribed for similar conditions helps suggest cost-effective alternatives.
```sql
SELECT medication_name, COUNT(customer_ID) AS prescriptions, AVG(dosage) AS avg_dosage
FROM medications
GROUP BY medication_name;
```
![image](https://github.com/user-attachments/assets/61479644-d8c9-46ed-a8b9-2179aee122e3)



**Key Insight:** Determines whether hospitals can promote cost-effective medications without compromising treatment quality.

---

## **Conclusion**

If you found this helpful, consider liking, staring or sharing. Your support means a lot!

- 👨🏽‍💻 [GitHub Profile](https://github.com/JoshuaSamuelNichols)
- 🌐 [Portfolio Website](https://joshuasamuelnichols.github.io/)
- 🔒 [Join the Privacy Movement with Proton](https://go.getproton.me/SH123)
- 📚 [Learn SQL, Python, and More on DataCamp](http://datacamp.pxf.io/LK2zJV)

---
*Fight until data_privacy = True*
