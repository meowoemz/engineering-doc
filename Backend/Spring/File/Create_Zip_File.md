```
public void writeZip(String file_name, String path_str) throws IOException {
        String path_zip = csv_path + file_name + ".zip";
        try {
            FileOutputStream fos = new FileOutputStream(path_zip);
            ZipOutputStream zos = new ZipOutputStream(fos);
            addToZipFile(path_str, zos);
            zos.close();
            fos.close();
        } catch (Exception e) {
            throw e;
        }

    }

    private void addToZipFile(String fileName, ZipOutputStream zos) throws FileNotFoundException, IOException {

        File currentFile = new File(fileName);
        FileInputStream fis = new FileInputStream(currentFile);
        String fn = rmPath(fileName);
        ZipEntry zipEntry = new ZipEntry(fn);
        zos.putNextEntry(zipEntry);

        byte[] bytes = new byte[1024];
        int length;
        while ((length = fis.read(bytes)) >= 0) {
            zos.write(bytes, 0, length);
        }

        zos.closeEntry();
        fis.close();
        currentFile.delete();
    }

    private String rmPath(String fName) {
        int pos = fName.lastIndexOf(File.separatorChar);
        if (pos > -1)
            fName = fName.substring(pos + 1);
        return fName;
    }
```

Note: if you don't remove the path directory in file name, whatever you put into zip entry, it would be default
    hierarchy in your zip file;
    
References:
   https://stackoverflow.com/questions/1091788/how-to-create-a-zip-file-in-java
    
    
   http://www.avajava.com/tutorials/lessons/how-can-i-create-a-zip-file-from-a-set-of-files.html