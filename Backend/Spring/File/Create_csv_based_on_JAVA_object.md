
```
public void writeTransactionsCSV(List<Object> objects, String path_str) throws IOException {
        try {
            BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(path_str), "UTF-8"));
            for (Object object : objects) {
                StringBuffer oneLine = new StringBuffer();
                oneLine.append(object.getId());
                oneLine.append(CSV_SEPARATOR);
                oneLine.append(object.getVendor_name());
                oneLine.append(CSV_SEPARATOR);
                oneLine.append(object.getAmount());
                oneLine.append(CSV_SEPARATOR);
                oneLine.append(object.getName());
                bw.write(oneLine.toString());
                bw.newLine();
            }
            bw.flush();
            bw.close();
        } catch (Exception e) {
            throw e;
        }
    }
```

References: 
    https://stackoverflow.com/questions/3666007/how-to-serialize-object-to-csv-file