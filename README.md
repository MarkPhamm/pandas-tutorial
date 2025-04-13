# Pandas Syntax Cheatsheet

This guide covers essential pandas syntax across data inspection, basic manipulation, aggregation, joins/unions, datetime operations, and null handling.

**Getting Started**

To get started with this project, follow these steps:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/MarkPhamm/pandas-tutorial.git
   cd pandas-tutorial
   ```

2. **Create a virtual environment**:
   ```bash
   python -m venv venv
   ```

3. **Activate the virtual environment**:
   - On Windows:
     ```bash
     venv\Scripts\activate
     ```
   - On macOS and Linux:
     ```bash
     source venv/bin/activate
     ```

4. **Install the required packages**:
   ```bash
   pip install -r requirements.txt
   ```

## 1. Data Inspection

### 1.1 View the first few rows
```python
df.head()
```

### 1.2 View the last few rows
```python
df.tail()
```

### 1.3 View column names
```python
df.columns
```

### 1.4 Access a single column
```python
df['col']
# or
df.col
```

### 1.5 Check the shape of the DataFrame
```python
df.shape
```

### 1.6 Check data types and non-null counts
```python
df.info()
```

### 1.7 Get summary statistics
```python
df.describe()
```

### 1.8 Check for duplicates
```python
df.duplicated().sum()
```

### 1.9 See value counts in a column
```python
df['col'].value_counts()
```

---

## 2. Basic Manipulation

### 2.1 Select specific columns
```python
df[['col1', 'col2']]
```

### 2.2 Filter rows using condition
```python
df[df['col'] > 100]
```

### 2.3 Filter rows using `.between()`
```python
df[df['col'].between(10, 50)]
```

### 2.4 Rename columns
```python
df.rename(columns={'old_name': 'new_name'})
```

### 2.5 Sort values
```python
df.sort_values(by='col', ascending=False)
```

### 2.6 Select rows using `.loc` (label-based)
```python
df.loc[5]
```

### 2.7 Select rows using `.iloc` (position-based)
```python
df.iloc[5]
```

### 2.8 Change datatypes using `astypes`
```python
df = df.astype({'col_name': 'desired_dtype'})
# or 
df['col_name'] = df['col_name'].astype('desired_dtype')
```

# Return all rows where the 'verified' column is NOT True
```python
df[~df['col'] == 'target']
```
---

## 3. Aggregation Functions

### 3.1 Group by and sum
```python
df.groupby('group_col')['value_col'].sum().reset_index()
```

### 3.2 Group by and count
```python
df.groupby('group_col')['value_col'].count().reset_index()
```

### 3.3 Group by and count unique values
```python
df.groupby('group_col')['value_col'].nunique().reset_index()
```

### 3.4 Group by with multiple aggregations using `.agg()`
```python
df.groupby('group_col').agg({
    'col1': 'sum',
    'col2': 'mean',
    'col3': 'nunique'
}).reset_index()
```

---

## 4. Join and Union

### 4.1 Merge two DataFrames on different keys
```python
df1.merge(df2, left_on='key1', right_on='key2', how='inner')
```

### 4.2 Merge using `how='left'`, `how='right'`, or `how='outer'`
```python
df1.merge(df2, on='key', how='left')
```

### 4.3 Union two DataFrames (like SQL `UNION ALL`)
```python
pd.concat([df1, df2], ignore_index=True)
```

### 4.4 Union with deduplication (like SQL `UNION`)
```python
pd.concat([df1, df2], ignore_index=True).drop_duplicates()
```

---

## 5. Datetime Functions

### 5.1 Create a timestamp
```python
pd.Timestamp('2025-04-12')
```

### 5.2 Create a time delta
```python
pd.Timedelta(days=30)
```

### 5.3 Convert a column to datetime
```python
df['date_col'] = pd.to_datetime(df['date_col'])
```

### 5.4 Extract day from datetime
```python
df['day'] = df['date_col'].dt.day
```

### 5.5 Convert datetime to monthly period
```python
df['month'] = df['date_col'].dt.to_period('M')
```

### 5.6 Calculate time difference in seconds
```python
(df['end_time'] - df['start_time']).dt.total_seconds()
```

---

## 6. Null Handling

### 6.1 Check for null values
```python
df['col'].isnull()
```

### 6.2 Filter rows with null values
```python
df[df['col'].isnull()]
```

