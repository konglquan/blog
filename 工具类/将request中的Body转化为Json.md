```java
    /**
     * 将request中的Body转化为Json
     * @param request
     * @return
     * @throws IOException
     */
    public static String getJson(HttpServletRequest request) throws IOException{
        BufferedReader streamReader = new BufferedReader(
                new InputStreamReader(request.getInputStream(), StandardCharsets.UTF_8));
        StringBuilder sb = new StringBuilder();
        String inputStr;
        while ((inputStr = streamReader.readLine()) != null) {
            sb.append(inputStr);
        }
        return sb.toString();
    }
```

