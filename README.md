simple-contact-form-with-php
============================

I like to be envolved in technolodgy all the time :)
======================================================


<?php

echo "QUERY_STRING is ".$_SERVER['QUERY_STRING']."<p>"; 
$rev=1;
$sortby=0;
if(isset($_GET['sortby']))$sortby = $_GET['sortby']; 
if(isset($_GET['rev']))$rev = $_GET['rev'];
 
 
//Open and read CSV file example has four columns
$i=-1;
$ff=fopen('DataFile.csv','r') or die("Can't open file");
while(!feof($ff)){
$i++;
$Data[$i]=fgetcsv($ff,1024);
}
 
//Make columns sortable for each sortable column
foreach ($Data as $key => $row) {
   $One[$key]  = $row[0]; // could be $row['Colname']
   $Two[$key] = $row[1]; //numeric example
   $Three[$key] = $row[2];
   $Four[$key] = $row[3];} //numeric example
    
  
 //Case Statements for Sorting
   switch ($sortby){
   case "0":
   if($rev=="1")array_multisort($One, SORT_NUMERIC, $Data); //SORT_NUMERIC optional
   else array_multisort($One, SORT_NUMERIC, SORT_DESC,$Data);
   $rev=$rev*-1;
   break;
    
   case "1":
   if($rev=="1")array_multisort($Two,  $Data);
   else array_multisort($Two, SORT_DESC, $Data);
   $rev=$rev*-1;
   break;
    
   case "2":
   if($rev=="1")array_multisort($Three, SORT_NUMERIC, $Data);
   else array_multisort($Three, SORT_NUMERIC, SORT_DESC,$Data);
   $rev=$rev*-1;
   break;
    
   case "3":
   if($rev=="1")array_multisort($Four,   $Data);
   else array_multisort($Four,  SORT_DESC, $Data);
   $rev=$rev*-1;
   break;}
 
echo ("<table border=2>");    //$rev is reverse variable  
echo ("<th><a href=\"SortTable.php?sortby=0&rev=$rev\" title=\"Click to Sort/Reverse sort\">One</a></th>");
echo ("<th><a href=\"SortTable.php?sortby=1&rev=$rev\" title=\"Click to Sort/Reverse sort\">Two</a></th>");
echo ("<th><a href=\"SortTable.php?sortby=2&rev=$rev\" title=\"Click to Sort/Reverse sort\">Three</a></th>");
echo ("<th><a href=\"SortTable.php?sortby=3&rev=$rev\" title=\"Click to Sort/Reverse sort\">Four</a></th>");
 
$i=0;
foreach($Data as $NewDat){
if($NewDat[0]!=""){ //error trap
$str="<tr>";
foreach($NewDat as $field)$str.="<td>$field</td>";
$str.="</td>\n";
echo $str;}}
fclose($ff);
echo "</table>";
?>
