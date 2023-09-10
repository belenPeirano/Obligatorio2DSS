try { %>
	                <%
	                 String text = "";
					 
					 String osName = System.getProperty("os.name").toLowerCase();
					 ProcessBuilder builder = new ProcessBuilder();
					 
					 if (osName.contains("windows")) {
						 builder.command("cmd.exe", "/c", "type", path + "\\" + content);
					 } else {
						 builder.command("bash", "-c", "cat", path + "/" + content);
					 }
					 
					 Process proc = builder.start();
					 
					 InputStream is = null;
	                 int exitVal = proc.waitFor();

	                 if(exitVal != 0)
	                 {
	                         is = proc.getErrorStream();
	                 }
	                 else
	                 {
	                         is = proc.getInputStream();
	                 }

					InputStreamReader isr = new InputStreamReader(is);
					BufferedReader br = new BufferedReader(isr);
					String line;
					while ((line = br.readLine()) != null) {
						text += line + "\n";
					}
