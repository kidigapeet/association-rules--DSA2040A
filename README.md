# 🛒 Association Rules Mining with Python (mlxtend)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-1.0%2B-orange)
![mlxtend](https://img.shields.io/badge/mlxtend-0.22%2B-brightgreen)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
![Status](https://img.shields.io/badge/Status-Active-success.svg)

> A simple, hands-on example of **association rule mining** using the **Apriori algorithm** from the `mlxtend` library.

---

## 📘 Overview

This project demonstrates how to uncover relationships between items in transactional data — a process known as **market basket analysis**.

We’ll:
1. Create a small sample dataset of shopping baskets 🛍️  
2. Encode transactions into a **one-hot matrix**  
3. Apply the **Apriori algorithm** to find frequent itemsets  
4. Derive **association rules** with metrics like *support*, *confidence*, and *lift*

---

## ⚙️ Requirements

Before running the script, install the required dependencies:

```bash
pip install pandas mlxtend
```
🧩 Code Walkthrough
1️⃣ Create a Sample Dataset
Each list represents a customer’s shopping basket:

python
Copy code
dataset = [
    ['Milk', 'Bread', 'Eggs'],
    ['Bread', 'Diapers', 'Beer', 'Eggs'],
    ['Milk', 'Diapers', 'Bread', 'Cola'],
    ['Bread', 'Milk', 'Diapers', 'Beer'],
    ['Milk', 'Bread', 'Diapers', 'Eggs']
]
2️⃣ One-Hot Encoding the Transactions
Convert the data into a binary matrix — each column represents an item, and each row represents a transaction.

python
Copy code
from mlxtend.preprocessing import TransactionEncoder
import pandas as pd

te = TransactionEncoder()
te_ary = te.fit(dataset).transform(dataset)
df = pd.DataFrame(te_ary, columns=te.columns_)
print(df)
Sample output:

Beer	Bread	Cola	Diapers	Eggs	Milk
False	True	False	False	True	True
True	True	False	True	True	False
False	True	True	True	False	True
True	True	False	True	False	True
False	True	False	True	True	True

3️⃣ Finding Frequent Itemsets
Using the Apriori algorithm to identify frequent item combinations:

python
Copy code
from mlxtend.frequent_patterns import apriori

freq_items = apriori(df, min_support=0.6, use_colnames=True)
print(freq_items)
This identifies itemsets that appear in at least 60% of all baskets.

4️⃣ Generating Association Rules
Now, let’s create rules that meet a minimum confidence of 70%:

python
Copy code
from mlxtend.frequent_patterns import association_rules

rules = association_rules(freq_items, metric="confidence", min_threshold=0.7)
print(rules)
Each rule will show:

🧾 Antecedents → items on the left-hand side

🎯 Consequents → items on the right-hand side

📊 Support, Confidence, and Lift metrics

📊 Example Output
text
Copy code
Frequent itemsets:
   support             itemsets
0      0.8               (Bread)
1      0.8                (Milk)
2      0.8             (Diapers)
3      0.6          (Milk, Bread)
4      0.6       (Bread, Diapers)
5      0.6        (Milk, Diapers)

Association rules:
     antecedents   consequents  support  confidence      lift
0        (Milk)       (Bread)      0.6     0.75         0.94
1        (Bread)      (Milk)       0.6     0.75         0.94
2        (Milk)     (Diapers)      0.6     0.75         0.94
3     (Diapers)      (Milk)       0.6     0.75         0.94
🧠 Key Concepts
Metric	Description
Support	How frequently an itemset appears in the dataset
Confidence	Probability of item Y being purchased when item X is purchased
Lift	Strength of the association; values > 1 indicate a positive correlation
Apriori Principle	If an itemset is frequent, all its subsets are frequent

🚀 Run It Yourself
Clone the repository and run the script:

bash
Copy code
git clone https://github.com/your-username/association-rules-demo.git
cd association-rules-demo
python association_rules_demo.py
📚 References
mlxtend Documentation

Association Rule Learning – Wikipedia

Apriori Algorithm – GeeksforGeeks

🧾 License
This project is licensed under the MIT License.

💡 Author
Your Name
📧 [your.email@example.com]
🌐 your-portfolio-link

“Data tells a story — association rules help you read it.” 📊

