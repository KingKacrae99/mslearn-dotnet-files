## Evidence 2:
* ### sales summary function

* using Newtonsoft.Json;
* var currentDirectory = Directory.GetCurrentDirectory();
* var reportDir = Path.Combine(currentDirectory, "Reports");
* var salesFiles = FindFiles(storesDirectory);
* var salesTotal = CalculateSalesTotal(salesFiles);
* var summaryReport = GenerateReportFile(salesFiles);

* string GenerateReportFile(IEnumerable<String> salesFiles)
* {
    * var salesSummaryFile= Path.Combine(reportDir, "sales_summary.txt");
    * int numbering = 1;
    
    * if (!File.Exists("sales_summary.txt"))
    * {
        * if (!Directory.Exists(reportDir))
        * {
          *  Directory.CreateDirectory(reportDir);
        * }
        * File.WriteAllText(salesSummaryFile,$"Sales Summary{Environment.NewLine}");
        * File.AppendAllText(salesSummaryFile,"------------------------------------------------");
        * File.AppendAllText(salesSummaryFile,$"{Environment.NewLine}Total Sales: ${salesTotal}* **{Environment.NewLine}");
        * File.AppendAllText(salesSummaryFile,$"\nDetails{Environment.NewLine}");
    * }

    * foreach (var file in salesFiles)
    * {
      *  string fileName = Path.GetFileName(file);
       * if(fileName != "salestotals.json")
        * {
          *  string salesJson = File.ReadAllText(file);
            
        
           * // Parse the contents as JSON
            * SalesData? data = JsonConvert.DeserializeObject<SalesData?>(salesJson);
            * var total = data?.Total;

            * File.AppendAllText(salesSummaryFile, $"{numbering++}). {fileName}: ${total}{Environment.NewLine}");
        * }

    * }

    * Console.WriteLine(File.ReadAllText(salesSummaryFile));
    * return "Successfully";
* }

