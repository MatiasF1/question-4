# question-4
url =  "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/stock.html"
html_data_2 = requests.get(url).text

soup = BeautifulSoup(html_data_2, 'html5lib')

gme_revenue = soup.find_all('table')
for index, table in enumerate(gme_revenue):
    if ("GameStop Revenue" in str(table)):
        index_gmestop_revenue = index
        gme_table_revenue = pd.DataFrame(columns=["Date", "Revenue"])

for row in gme_revenue[index_gmestop_revenue].tbody.find_all("tr"):
    col = row.find_all("td")
    if (col != []):
        date = col[0].text
        revenue = col[1].text.replace("$", " ").replace(",", " ")
        new_row = pd.DataFrame({"Date": [date], "Revenue": [revenue]})
        gme_table_revenue = pd.concat([gme_table_revenue, new_row], ignore_index=True)

gme_table_revenue["Revenue"] = gme_table_revenue['Revenue'].str.replace('|\$' ,"")

gme_table_revenue.dropna(inplace=True)

gme_table_revenue.tail()


![Captura de pantalla 2024-09-22 194329](https://github.com/user-attachments/assets/cb3a5e4a-2c34-4b90-a91f-d3df56bb0d02)
![Captura de pantalla 2024-09-22 194405](https://github.com/user-attachments/assets/2867cd78-69e6-4f08-a385-908c41245e31)
