```
@GetMapping("/download/{extract-token}")
    @ResponseBody
    public ModelAndView download(HttpServletRequest request, HttpServletResponse response, @PathVariable(value = "extract-token") String token) {

        ATDownload currentDownload;
        try {
            currentDownload = atDownloadService.getDownloadByToken(token);
        } catch (Exception exception) {
            return new ModelAndView("redirect:/error.html");
        }
        //tell browser program going to return an application file
        //instead of html page


        try
        {
            File f=new File(currentDownload.getLocation());
            response.setContentType("application/zip");
            response.setHeader("Content-Disposition","attachment;filename="+currentDownload.getFile_name());
            response.setHeader("Cache-Control", "no-cache");
            byte[] buf = new byte[response.getBufferSize()];
            response.setContentLength((int)f.length());
            int length;
            FileInputStream fis = null;
            BufferedInputStream fileInBuf = null;

            fileInBuf = new BufferedInputStream(new FileInputStream (f));

            ByteArrayOutputStream baos = new ByteArrayOutputStream();

            while((length = fileInBuf.read(buf)) > 0) {
                baos.write(buf, 0, length);
            }

            response.getOutputStream().write(baos.toByteArray());
            response.getOutputStream().flush();
            response.getOutputStream().close();
            f.delete();
        } catch (Exception exception) {
            return new ModelAndView("redirect:/error.html");
        }
        return null;
    }
```

in this case, we use additional data structure to support download, this is not mandatory step

References:
    https://www.webdeveloper.com/forum/d/118654-download-a-zip-file-from-server-to-local-machine