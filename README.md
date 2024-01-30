import matplotlib.pyplot as plt, seaborn as sns

# Menghitung jumlah baris dan kolom subplot
num_variables = len(catVar.columns)
num_cols = 3
num_rows = int(np.ceil(num_variables / num_cols))

# Membuat grid subplot
fig, axes = plt.subplots(nrows=num_rows, ncols=num_cols, figsize=(20, 5 * num_rows))

# Menampilkan countplot untuk setiap kolom kategorikal
for i, ax in enumerate(axes.flatten()):
    if i < num_variables:
        col = catVar.columns[i]
        # Jika kolom kategorikal adalah data Boolean
        if catVar[col].dtype == 'bool':
            ax = sns.countplot(y=col, data=catVar.astype({col: 'object'}), ax=ax, order=catVar.iloc[:, i].value_counts(ascending=False).index)
        # Jika kolom kategorikal adalah data numerik
        else:
            ax = sns.countplot(y=col, data=catVar, ax=ax, order=catVar.iloc[:, i].value_counts(ascending=False).index)
    else:
        # Menghapus subplot yang tidak digunakan
        fig.delaxes(ax)

# Menampilkan grafik
plt.tight_layout()
plt.show()
