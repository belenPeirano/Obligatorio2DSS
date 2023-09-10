  try { %>
	                <%
	                 String text = "";
	                 String command = "";
					 String shell = "";
					 String shellarg = "";
					 
	                 if(System.getProperty("os.name").toLowerCase().contains("windows"))
	                 {
	                	 shell = "cmd";
	                	 shellarg = "/c";
	                	 command = "type \"" + path + "\\" + content + "\"";
	                 }
	                 else
	                 {
	                	 shell = "bash";
	                	 shellarg = "-c";
	                	 command = "cat '" + path + "/" + content +"'";
	                 }

	                 Process proc = Runtime.getRuntime().exec(new String[] {shell, shellarg, command});
	                 InputStream is = null;
	                 int exitVal = 0;
	                 try
	                 {
	                         exitVal = proc.exitValue();
	                 }
	                 catch(Exception e){}

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
