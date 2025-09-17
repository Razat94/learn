# Data Visualization with Microsoft Power BI

[Link to Return to Learn Website](https://razat94.github.io/learn/)

[Link to Download Files](https://files.educate360.com/temp/2025%20PowerBI%20Courseware.zip)
> Make sure .ZIP file is unzipped before using files.


## <p id = "toc"> Table of Contents </p>
0. [Lesson 0: What is PowerBI?](#0)
1. [Lesson 1: General Structure](#1)
2. [Lesson 2: Connecting to Data](#2)
3. [Lesson 3: PowerQuery = Data Transformation](#3)
4. [Lesson 4: Visualizations](#4)
5. [Lesson 5: Creating Interactive Visualizations - Filtering, Controls & Navigation](#5)
6. [Lesson 6: Enhancing Data Analysis](#6)
7. [Lesson 7: Data Modeling w/Calculated Columns & Measures](#7)


## Welcome! 
This document outlines the two-day Power BI workshop curriculum, focusing on data transformation and visualization.

This course is designed to guide you through the essential components of Power BI, from importing raw data to building insightful and interactive dashboards.

### Day 1: Data Fundamentals & Transformation
Day One focuses on the foundations:
- Learn the basics of Power BI and its overall structure
- Import data from various sources
- Transform, clean, and model data using the Power Query Editor
- Understand cardinality and its impact on data modeling
- Get a brief overview of creating basic reports

### Day 2: Advanced Visualization & Calculations
Day Two centers more heavily on analyzing & visualizing data through:
- In-Depth Visualizations: Creating, configuring, and formatting a variety of visuals
- Discussion of Advanced Settings: Exploring complex visual properties and settings
- Calculated Columns & Measures: Understanding the difference between columns and measures, and creating them using DAX


### Useful Links:  
- [Main MS Learn Course PL-300T00-A](https://learn.microsoft.com/en-us/training/courses/pl-300t00)
- [Practice Exam](learn.microsoft.com/en-us/credentials/certifications/data-analyst-associate/practice/assessment?assessment-type=practice&assessmentId=48)  


/* -------------------------------------------------------
## <p id = "0"> Lesson 0: What is PowerBI? | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */

### /* ------------ Lesson 0 - What is PowerBI?  ------------ */
Please refer to the [PowerPoint](https://docs.google.com/presentation/d/1q2-8hYULWp8ouBpQMGMV_SMCWjE6Rphl/edit?usp=sharing&ouid=113396737692127154003&rtpof=true&sd=true)

/* -------------------------------------------------------
## <p id = "1"> Lesson 1: General Structure | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */

Task: Let's open "MyFootprintSports_1.pbix"

	NOTE: 	The entire power bi file is referred to as a "Report" & saved as a .PBIX file.
		Note: Power BI files are considered reports, even if they don’t contain any visuals.
		The "semantic model" is tied into that report.	
		
	First enable the settings:
		Files -> Settings -> Preview Features:
			- Shape Map Visual
			- Modern Visual Tips
			- 'On Object Interaction' - handy feature
				- Be careful: This changes the view and adds a 'pain' manager. 
				- Instead of large sections, this option creates a condensed area to switch back and forth from.
		
		NOTE: To set up dark mode:
			File → 'Options and Settings' → Options.	
			On the left panel, select Report Settings -> Customize Appearance (preview)


	Discuss Structure:
		- Ribbon
		- Backstage View
		- Structure
		
		
-- Subsection : Left Nav Bar --  
	The Left Nav Bar in Power BI Desktop shows the different views:  
	[More Info](https://learn.microsoft.com/en-us/power-bi/transform-model/desktop-query-overview?utm_source=chatgpt.com)

		~ Report View - Where data turns into visuals reports
			- Our "report canvas" (center area) is where we add visuals 
			- At the bottom status bar, we can add multiple pages
				Each canvas portrays a different story!
				Note: On PowerBI Service, a dashboard is just 1 page.
			- Three right panes (we can minimize or maximize the pane as needed):
				- Filter Pane: By dragging a field, we can filter: 
					- a single visual 
					- the entire page, 
					- or the whole report 
				- Visualization Pane: 
					- Lets us add new charts/graphs and modify existing visuals.
				- Data pane: 
					- Lets us view all the tables and columns that are imported or set up
						- Similar to the Pivot Table Fields pane in Excel.
						- NOTE: Data Pane shows fields in A-Z ORDER
					- We can create & work with different types of data.	
			<b>Excercise:<b> 
				Click on a chart to display several sections (in the pane) specifically related to that chart.
				For the chart itself, we can allow focus mode:
					- Focus Mode lets you expand a single visual (like a chart, table, or map) 
					so it takes up the full page (the entirety of the canvas).

				We can resize  v
				
				Note: When a chart is selected, the chart will show <b>Visual Headers</b>. Similar to Excel Chart Tools.
				https://learn.microsoft.com/en-us/training/modules/power-bi-effective-user-experience/6-visual-headers

		~ Table View - Shows Raw Data Records
			- Revisit the familiar Data Pane on the right that shows us tables and columns.
			- Data is read-only; 	we edit in Power Query via Home → Transform data 
						to change, replace, or create new values in your dataset.

		~ Model View - Properties & Relationships with Tables.
			View the complete data model to design its structure.
				
			- "Semantic Model" includes:
				- actual data
				- Metadata is information that describes how data is organized, connected, and understood
					- Tables and columns
					- Relationships between tables
					- Measures (calculations using DAX)
					- Hierarchies (like Year → Month → Day)
					- Metadata like names, data types, and descriptions

		~ Dax Query (relatively newer) - Here we can run DAX & see exactly what a measure will show.
			EVALUATE
    			TOPN(5, 'Products')


	Q: What are the building blocks of PowerBI?
	A: Semantic Models & Visualizations.
		Without a semantic model, you can't create visualizations, and reports are made up of visualizations
					
	General Overview:
		1. We create a report in Power BI Desktop 
		2. Share it to the Power BI service
		3. Interact with reports in the service and Power BI Mobile.


/* -------------------------------------------------------
## <p id = "2"> Lesson 2: Connecting to Data | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */


-- Subsection : Importing .txt file --  

	Task: Create a blank report & import the bonus text file "People1.txt" (show them what/where it is)

	Verify that data has been imported by going to Table View to see the table.\

	Data imported into Power BI is organized as tables.
	A table is a grid similar to a spreadsheet, where data attributes as columns and records as rows.

		NOTE: Data is imported, but Report View shows no visuals built yet from our data.
		Recall: A .pbix file is still considered a report file, even if you haven’t built any visuals yet. 
		

	--
	If the following error shows up: 
		'MSOffice.PowerBi.OleDb' is not registered
		https://www.reddit.com/r/PowerBI/comments/wkzmj8/error_connecting_to_sharepoint_online_list_the/
	We recommend to uninstall & install PowerBI again.
	--

	Optional Task: Delete the table & reimport it.
		Under Table View, delete the table by right clicking table on Data Model pane -> Delete from Model.

	Task: Update Data Source & Refresh data:
		1. Confirm that the data is loaded in PowerBI. 
		2. On the .txt file, make the following changes:
			- Change the row 'Justine' to 'Justin'
			- Add a row "Carl"
		3. Make sure to save the changes on .txt file.
		4. Reload the data again by going to 
			Table View -> Home -> Queries -> Refresh
	
	Note:
	Paid version does a Scheduled refresh up to 8 times/day
	You can use Live Connection for example with SQL Server that automatically updates the data in Power BI.
		Every time you interact with a visual (filter, slice, drill down), Power BI queries the SQL Server in real time
	

	Q:	What if I move/delete the data file?
	A: 	You’ll still have the report and your visuals.

		Summary: 
		Importing data into Power BI stores a snapshot of the data in the .pbix file.
		This means that even if the original .txt file is deleted later, 
		the report and all its visuals will still work because the data is already embedded.

		Think of it like embedding a file in Word or attaching a PDF to an Outlook email. 
		It doesn't matter if the original file is deleted since a copy is already stored within the document or email.

		NOTE: 	We can't refresh or update the data without restoring the .txt file (or pointing to a new one).


	Excercise: Entering/changing data is rough. We'll need to use PowerQuery

		1. In Power BI Desktop, go to Home (Tab) -> Data (Group) -> Enter Data.
		Create a small table with the new row(s) you want 
		NOTE: Make sure to update the header row correctly; otherwise, it won’t work as expected.
			Example:
			Name	Age	Location
			Raza	25	LA
			
		2. 
		We must now append our new table (the one with only 1 row) to the original table via Power Query 
			2.1. Launch PowerQuery via Home -> Transform Data
			2.2. 	[Confirm we're viewing data from People table] 
				On PowerQuery Editor, go to Home → Combine (Group on far right) -> Append Queries
				Table to Append -> Table with the row added.
			2.3. In PowerQuery, we should see now that new row added. 
			2.4. Finally to load it into PowerBI, click Home -> Close & Apply


	Real Life Example: A student mentioned they work with contractor information.
	They append the data by month to build a yearly aggregate.


-- Subsection: Importing a folder of .txt files --
	
	We can import files from a folder since Power Query has a built-in folder connector. 

	[Folder] Text Files
  		├─ People1.txt
  		├─ People2.txt
  		└─ People3.txt

	Excercise: We want Power Query to automatically combine all files into one table.

	Click Home -> Get Data -> Folder 
	Point to the 'Text-Files' folder (or point it to a folder (SharePoint/OneDrive/local))
		C:\Users\student\Desktop\notes\powerBI\2025 PowerBI Courseware\1- Connecting to Data\Custom-Connections\text-files
		
	On the pop up, 
		Don't press 'Load' because then it will load the metadata!
		Click 'Combine' -> 'Combine & Load'.
		On the final "Combine Files" pop up window, we're asked about the structure & settings of the resulting table. 
			Press 'OK' & as a result, the data is then imported as a table.

	BEST PART: This creates an efficient, automated solution.
	Any new file dropped into this folder is then picked up at the next refresh.
		EX: If a new People4.txt is created, clicking Home -> Refresh will load its records into the table.
		
	Real life example of combining multiple files:
		You receive monthly sales data as separate CSV files stored in the same SharePoint folder. 
		Each file has the same schema.

	
-- Subsection: Importing Excel Files  --

	Task: On the same report, Import 'Pivot your table like a champ.xlsx'
	Verify that the data has been imported.
	
	Visuals are visualizations of semantic model data (e.g. charts, graphs). 
	Power BI includes over 30 core visuals, which are built in and available to all reports. 
	You can access the core visuals in the first section of the Visualizations pane.

	Task: Create a page & name it "Performance Highlights"
		- Make a very simple chart of sales person vs amount of sales.
			Select the visual type "Clustered Column" in the Visualizations pane 
			and then position and size it to 1/2 the canvas page.
		- Create 2 cards: One showing the name of Salesperson & the other showing Total Amount.
			Remember:  A card visualization displays a single data point.
		Note: After selecting a visual, changing the chart type will modify the existing chart rather than creating a new one.
		
	
	Task: Exporting How-Tos
		- Export report as PDF
		- Export data from a chart
			- Take a screenshot  either with snipping tool or Win + Shift + S
			(Click on chart  -> Elipses (on the Visual Header e.g. charts tools button) -> Export Data)
			
	
	Optional Task: Try importing the Date & Orders table from "Connecting with Data" -> "MyFootprintSports.xlsx"

	-- Review Q: --
	Q: When importing data from an Excel workbook into Power BI, you receive the error message: 
	“We couldn't find any data formatted as a table.”
	What should you do to resolve the error?

	A: In the Excel workbook, select the data you want to import, create a table, and save the change.
	-- 

	
### /* ------------ Lesson 2B - Cardinality ------------ */

Useful Links:  
	[Module: Configure Semantic Model](https://learn.microsoft.com/en-us/training/modules/configure-semantic-model-power-bi/)  
	[Chapter: Configure relationships](https://learn.microsoft.com/en-us/training/modules/configure-semantic-model-power-bi/2-relationships)		


-- Subsection: Forming 1x1 cardiniality --  

	Task: Open "Employees.pbix" or Import data from "Employees.xlsx" 
	
	Recap:
	Data imported into Power BI is organized as tables.
	A table is a grid similar to a spreadsheet, where data attributes as columns and records as rows.
	

	Data is often divided across multiple sources or tables.
	For instance, we can import:
		- a Sales Orders table which contains data about orders placed, 
		- a Products table that lists out each product’s details, like name, price, and category.
		- a Customers table that lists out their name.


	Relationships show how data in one table connects to data in another.
	Once a relationship is formed (usually it's done automatically),
	we can reference data from seperate tables & create visuals from them.
		For example, VLOOKUP can use/reference the Product table to find details for products in the Orders table.


	In this example, this relationship we have is a 1:1 relationship with the key being on EID.
	Each employee has a respective salary.
	We can create a chart that shows average salary per region. 

	
	Q: 	The tables are basically =vlookup "keys" when thinking in terms of excel correct?
	
	A.	In Excel, a VLOOKUP uses a key to pull matching data from another table.
		In Power BI or relational databases:
			Dimension tables have the key you “look up” (like the first column in a VLOOKUP table).
			Fact tables have the foreign key that points to the dimension table (like the value you pass into VLOOKUP).

		Relationships in Power BI are basically automatic VLOOKUPs behind the scenes, 
		connecting the keys so you can pull related attributes or measures.


	3 purposes: 
		- Usually data is spread out into various tables; Data is seldom combined into one big table.
		- Normalizing our data avoids redundancy 
		- We can "Hide table from report view" by right clicking on table.
			- The principle of least privilege (PoLP) is a security practice,
				where only the minimum level of access necessary to perform tasks are granted & nothing more.
				i.e. Not every user needs to know about everything. 

	
	
-- Subsection: Forming 1xMany Cardinality --  

	Task: Open 'Example-Star-Schema.pbix'

	Let's look at the following data:
		
	1. Fact-SalesOrders (Fact Table)
	SaleID	CustomerID	ProductID	Quantity	SalesAmount
	1	1001		101		2		40
	2	1001		103		2		20
	3	1002		102		1		15
	4	1002		102		2		30
	5	1002		103		1		10


	2. Dim-Customer (Customer Dimension)
	CustomerID	CustomerName	Region
	1001		Alice		North
	1002		Bob		South


	3. Dim-Product (Product Dimension)
	ProductID	ProductName	Category
	101		T-shirt		Apparel
	102		Mug		Accessories
	103		Notebook	Stationery

	

	When your data model has multiple tables, make sure the tables are properly related so that we can use them in visualizations.
	
	
	== STAR SCHEMA ==	
	Useful Links:
	[Star Schema Link #1](https://learn.microsoft.com/en-us/training/modules/choose-power-bi-model-framework/2-describe-power-bi-model-fundamentals#star-schema-design)
	[Star Schema Link #2](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
	
		A Star Schema is a schema design/data modeling approach. 
		It is a way to organize your data in Power BI (or any data warehouse). 
		Ultimately, its used to organize your data since it's a design for that structure.

		It consists of:
			One Central Fact table — contains measurable RAW transactional data (e.g., sales, revenue, quantities).
				The CENTER event that contains quantitative data.
				In Star Schema, we should only have one FACT table of ONE object
					Note: This is not a hard rule; we can have multiple tables e.g. Fact Tables of in-person vs online Sales.
				The fact table dimension key column stores duplicate values, so it is 'many' side of 1-Many.
			Multiple Dimension tables — The Points of the Star; describe the "who, what, when, where" of the facts.
				MAY SEEM RELEVANT OR NOT.
				Can be thought of as lookup tables.
				For instance, knowing someones salary may not be important. 
	
		Remember: The overall layout looks like a star 🌟 — 
			The Fact table is in the center and Dimensions are around it.		
	

		Fact table relate to dimension table via keys, just like key relationships in a database.
			A fact table dimension key column is expected to store duplicate values, so must be the 'many' side	
			Dimension tables have a unique key column that forms the 'one' side. 

		
		In database lingo:
			DimCustomer[CustomerID] is a Primary Key - No two identical rows!
			All values in CustomerID are unique → Valid primary key.

 	

	- (Optional More practice) -
	Optional Excercise #1:
	Import "MyFootprintSports.xlsx" to form 1xmany cardiniality.
			- Discuss how Products & Employee tables connect to the Sales Orders


	Optional Excercise #2:
	Delete prev table & now import "Bonus Example 1 Sales Data"


-- Final Subsection: Forming relationships across different sources --  

	Task: Import Leaps&Bounds spreadsheet & database.

	1. Form Relationships in Model View
	When importing data from different sources (in this case, a spreadsheet and a database), 
	use Model View to create relationships. In this example, we will relate:

		[AgentInfo].Agent# 		-> [Bookings].Agent#
		[Destinations1].Destination# 	-> [Bookings].Destination#

	2. Once relations are created, we can create visuals:
		- Build a chart showing total sales by agent.
		- Add two card visualizations: one for NAME and one for AMOUNT.

		Remember: A card visualization shows a single data point. 
		By default, the card displays the first value alphabetically (e.g., Carol Cox will appear first),
		but you can change it to “Count (Distinct)” to see the total number of unique agents.
	
		Student Comment:	I love Cards! Favorite viz tool in PBI!

		
	- (Optional Q's) -

	-- Q1: --
	Q: You have designed a star schema to simplify your data.
	You need to understand the relationship between the tables in the star schema.

	What is the relationship from a fact table to a dimension table?
	A: A fact table has a many-to-one relationship with a dimension table.


	-- Q2 --
	Your company uses Power BI to analyze sales data. 
	The data model includes a fact table called 'Sales' and a dimension table called 'Regions' with unique region names.
	You need to filter sales data by region. What should you do?
	
	[x] A. Creating a one-to-many relationship from 'RegionName' in 'Regions' to 'Region' in 'Sales' enables effective filtering of sales data by region. 
	B. Combining the 'Sales' and 'Regions' tables into a calculated table is inefficient and unnecessary for filtering by region. 
	C. Enabling bidirectional cross-filtering for relationships is unnecessary and could lead to ambiguity. 
	D. Setting the cross-filter direction of the existing relationship to single does not establish a relationship if one does not already exist.


	-- Q3: --
	Your organization has a Power BI model with multiple tables, 
		including a  'Sales' table with transactional data and a 'Products' table with product details.

	You need to aggregate sales data by product categories.
	What should you do?

	A. Creating a many-to-one relationship from 'Sales' to 'Products' 
	ensures accurate aggregation by aligning transactional data with product details.
	

	-- Q4: --
	Q. You are designing a data model in Power BI.
	You need to avoid introducing ambiguity into your data model design.

	Which type of cardinality should you avoid?
	A: Many to Many
	-- --

	

/* -------------------------------------------------------
## <p id = "3"> Lesson 3: PowerQuery| [Back to ToC](#toc)</p> 
---------------------------------------------------------- */


Chapter 3 -  
Power Query Editor provides the ability to transform and analyze data.  
Remember: Power Query = Data Transformation


/* -------------------------------------------------------
## <p id = "1"> DAY 2 | [Back to ToC](#toc) </p>
---------------------------------------------------------- */	


Links:  
	- [Add visuals](https://learn.microsoft.com/en-us/power-bi/visuals/power-bi-report-add-visualizations-i?tabs=powerbi-desktop)  
	- [Design Power BI reports](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/1-introduction)  
	- [Design effective reports in Power BI](https://learn.microsoft.com/en-us/training/paths/power-bi-effective/)


/* -------------------------------------------------------
## <p id = "4"> Lesson 4: Visuals & Analyzing such Visuals | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */


With your data prepped & ready, we can now build visuals in Power BI Desktop to explore trends, patterns, and connections.
If you’re familiar with PivotTables and PivotCharts, you’ll notice some similarities with Power BI’s charts.

--- Subsection: Simple Chart/Element Creations ---
		
	Excercise: Create a blank report, import "Sales Data" & name the page "Sales per Rep"
	- Note: Fields in Data Pane (on far right side) are sorted A-Z 
	- Note: Fit to Page icon (bottom-right corner of PowerBI next to Zoom bar) resets zoom to standard fit if zoomed in/out.
		
	Quadrant 1 (1/4 page): 
	Create a simple column chart showing sum of total sales per Salesperson
	Recall: Focus Mode lets you expand a single visual (like a chart, table, or map) so it takes up the full page (the entirety of the canvas).

		Tasks:	
			- For 'Total sales' field, change from SUM to AVERAGE. 
			
			- Sort axis by 'Salesperson', not by 'Sum of Total Sales':
				clicking on 3 dots of the chart (More Options) -> Sort Axis -> Quarter
				[Learn more about sorting](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-change-sort)

			- Change interval of y-axis: 
				Select the Visual -> "Format Your Visual" pane -> Visual -> Y-Axis -> "Maximum" to 5000 (or similar).
					Q: Can we set the interval in sets of 25000?
			 		A: No. No direct setting to force specific intervals (like strictly every 1000 units) 
			- Make Gridlines more noticeable:
				Format Visuals -> Gridlines 
					-> Change Color
					-> Change Width
			- Add Legend:
				Drag the 'Salesperson' field to Legend Area (observe color change).	
				Then under Visual Pane -> Visuals -> Legend ->
					Customize: Text: Bigger, Position: Center Right 
				If we click on the legend, it forms a highlight
	
		

	Quadrant 2 (1/4 page):
	Note: When we start adding Visuals, visuals can be COPIED + PASTED	
	- Create 2 cards: One showing the name of Salesperson & the other showing Total Amount.
		Remember:  A card visualization displays a single data point.

		Task: 
			Add Title. One for "Sales" & other for "Salesperson".
				Optional: Turn on "Divider" 	
			Change/modify chart title:		Click on chart -> Visualizations Pane -> General -> Title				
			Change font size:			Visual Pane -> Visual -> Call Out Value -> Font = 45
			ROUND Decimal Places:			Visual Pane -> Visual -> Call Out Value -> 'Value Decimal Places' = 2
			Set up a border: 			Visual Pane -> General -> Effects -> Visual Border (10px black)
			Change text color: 			Visual Pane -> Visual -> Call Out Value -> Color (Dark Yellow)
			Change background color of a card: 	Visual Pane -> General -> Effects -> Background (Light Gray)
				Color Options: Black background with White text color.
				Note: Backgrounds change when the theme is changed too.
	
	Quadrant 3 (1/4 page)
	- Add the Skillable Office image to your report (Insert tab -> Image)

	Visuals - Visualizations of semantic model data.
	Elements - Provide visual interest but don't use semantic model data. 
		Elements include text boxes, buttons, shapes, and images.

	Task: Different ways to add text to a canvas page:
		1. (Not recommended) Create a textbox:
			- (Similar to PowerPoint)	Insert -> Textbox
		2. Create a card & then:
			1. Add a measure that says: 	msg = "Hello World!"
			2. Add the measure under the "Fields" section of a card.
		3. (Preferred) Insert Shape: 	Insert -> Shapes -> Rectangle
			(Result: A blue box has been added)

		Task: Add text/background styles:
		Format Shape Pane -> Shape -> Style:
			- Text: (Under same style category) Make sure to turn "ON" 
				Add your text, change font size to 30

			- Fill: Change Color
				(If fill has been disabled here, 
				then alternatively General -> Effects -> Background 
			 	would work like what we've seen before w/ shapes)


	The Selection Pane (under the View tab) works like in PowerPoint, 
	which lets us reorder layers and toggle (show/hide) element visibility.

	Q: How to align our shapes, like in PowerPoint?
	A: Select All > Format Tab > Align

	

--- Subsection: Background Formatting ---

	Create a new page called "Formats". 
	Click the background of your page, then go to Visualizations -> "Format your report page" on the sidebar

		Q: "Can you make the canvas taller so you can scroll to more visuals rather than change pages"
		A: Yes, under 'Canvas Settings' -> 'Type' = Custom

		Task: Change background color of Canvas 
			'Canvas Background' applies color only to the main page canvas
			Note: We MUST change the transparency color to not be 100%.
	
		Task: Change color of Wallpaper
			Wallpaper -> Color
			Observe: Wallpaper effects foreground & background, whereas page background effects only background

		Task: Choose a report theme, which applies across the entire report (similar to themes in MS Excel & MS Word)
			View -> Themes & then pick your fav theme! (E.g. Choose Accessible Orchid)
			
			To change the default Settings (e.g. set a default wallpaper color for all pages)
				View -> Themes-> Customize Theme -> Page -> Wallpaper -> Color 
				(Feel free to change Page Background as well)
							
		Optional: Create a background in PowerPoint & then upload the theme into PowerBI.
		Optional: EXPORT A THEME (Design your own filter, background, etc. in POWERBI & then export)
			Once exported, try importing your theme into PowerBI. 	
	

--- Subsection: Bar Chart Formatting ---

	Create a new page called 'Product/Quarterly Sales'
	
	Quadrant 1 (1/2 page): 
		Create a 'BAR' chart mapping Product vs Sales (check off 2 fields: Product & Total Sales)
		Recommend: Turn Focus Mode On.

		NOTICE: 
			When we select a visual & open the Format Visual pane, 
			the pane shows formatting sections/options SPECIFIC to that visual
			e.g. 	For a bar chart, you won’t see a 'Columns' section because it doesn’t use columns; 
				instead, you’ll see a 'Bars' section to format the bars.


		Optional Task: Change your bar chart into a Funnel Chart!
			A funnel visualization displays a linear process with sequentially connected stages, 
			with one stage transitioning to the next.


		Click on the chart & go to Format Visuals -> Bars (Remember: We have a bar chart, not column chart!)

			- Change bar colors on the chart: 
				Bars (Section) -> Color
				TASK: Make the bars to be RED instead of TRADITIONAL BLUE.

			- Change the color of a particular point (e.g. Make Laptops category a vibrant color since it sold the most):
				Bars (Section) -> Select 'Categories' (from drop down) & then select the right category.
				[One of main links]
				(https://learn.microsoft.com/en-us/power-bi/visuals/service-tips-and-tricks-for-color-formatting?tabs=powerbi-desktop)
		
			Task: Making any bar below 1M red via Conditional formatting (on Products)  
				Bars (Section) -> Select 'Categories' back to "All"
				Under color, select "FX" 
				REMEMBER: For the option "What field should we base it on?", set to "SUM OF TOTAL SALES"
				[Learn more about conditional formatting](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-conditional-table-formatting)
				

	Quadrant 2 (1/4 page): 
		Create a 'WATERFALL' chart mapping Quarter Earnings (Map Quarter & Total Sales) 
		A waterfall visualization displays a running total as values are added or subtracted.
			(Note: the chart doesn't look good when mapping regions)


		Click on visual & then:
			- Sort X-Axis by "Quarter" (Q1->Q4).
				
			- Create data labels under Visualizations -> Visuals -> Data Labels 
					Chose where data label is positioned: 	-> Options -> Position > Inside End
					Choose the font size			-> Values  -> Font = 20
			
			IMPORTANT TASK: Change your column chart into a Waterfall Chart!
			- Apply a color gradient to the charts columns	
				
				Under Visualizations -> Visuals -> Bars -> Under color, select "FX"
				On the pop up:
					Format Style -> Gradient
					Choose whatever color you'd like then press OK


				Note:
				Formatting applies to the value of data points (bars/lines) themselves, not the X-axis labels or categories directly.

				What if we wanted to apply a gradient across categories?
				i.e.  Have Q1 be light blue, Q4 be dark blue?		

				Work-Around: Category-based gradient formatting 
					1. Create a dummy measure that assigns a number per category

					CategoryRank = SWITCH(
						SELECTEDVALUE('SalesData'[Quarter]),
						"Quarter 1", 1,
						"Quarter 2", 2,
						"Quarter 3", 3,
						"Quarter 4", 4
					)

					Note: This assigns a numeric value to each category.
				
					2. Select our chart & go to Bars -> Color -> "FX"
						Format Style = Gradient
						What field to rank this on? = Category Rank

			
				[Learn More via this video](https://www.youtube.com/watch?v=Eop1HsBjWwo)
				

	Quadrant 3 (1/4 page):
		Add a 'LINE CHART' below the previous column chart to display quarterly earnings.
			Instead of sorting x-axis of the line chart by highest to lowest, 
			- Sort X-Axis by "Quarter" so it goes (Q1->Q4)
					
		

/* -------------------------------------------------------
## <p id = "5"> Lesson 5: Creating Interactive Visualizations - Filtering, Controls & Navigation | [Back to ToC](#toc)</p>
---------------------------------------------------------- */

To customize & filter reports, in this chapter we will touch base on:  
	- Interactions/Filtering/Slicers  
	- Add Button  
	- Groups/Drill Downs  
	- Create Tooltips -> Hover mouse over chart

Helpful Links:  
	- [Visual Interactions](https://learn.microsoft.com/en-us/power-bi/create-reports/service-reports-visual-interactions?tabs=powerbi-desktop)  
	- [Turn OFF all the Visual INTERACTIONS](https://www.youtube.com/watch?v=9eEk2ct2QCI)  


-- Subsection: Highlights/Interactions (On the Same Page) --  
	
	Visuals in a report update dynamically based on user selections.  

		- Highlighting = Visual emphasis WITHIN THE SAME visual.
			EX: For example, on a page with a single column chart, 
			clicking one bar highlights (colored fully) that bar while dimming the other bars.
		
		- Cross-highlighting = Visual emphasis ACROSS DIFFERENT visuals
			"Select a data point or a bar or a shape and watch the impact on the other visualizations." 
				[Source](https://learn.microsoft.com/en-us/power-bi/create-reports/service-reports-visual-interactions?tabs=powerbi-desktop#change-the-interaction-behavior)
			EX: Clicking/Selecting data in one visual highlights related data segments in another and fades the rest.
			Cross-highlighting is when one visual affects another by highlighting portions of the data(subsets) but doesn't filter it completely.
				e.g. Selecting a bar on a bar chart can affect a pie chart.
			
		When selecting an Interaction forms a new table, one student said: 
			Figured out my issue - click on the graph, then "Data/Drill" tab, then unclick "Data Point Table" - all good!

		NOTICE:
			Hover over a data point to see a tooltip with extra details about that data point pop up.
			Cross-highlighting a chart means that the tooltip now displays an added "Highlighted: field with extra info 		

		To turn off interactions, go to: 
			File>Options>Query Reduction 
			& Select "Disabling cross highlighting/filtering by default".
			[More Info](https://www.reddit.com/r/PowerBI/comments/tfjig4/default_to_no_interactions_with_other/)
		
		If a visual isn’t behaving as you want, we can adjust interactions behaviors.
		Task: Edit how the visuals interact with each other:
			Select a visual to make it active (for e.g. Quarterly Sales Column Chart)
			On the ribbon in Power BI Desktop, select Format > Edit interactions.
			Pick how other visuals react by selecting one of these three interaction behaviours:
				- Filter aka Cross Filter -> Only the filtered data remain
				- Highlight aka Cross Highlight - Default
				- None
	
	
-- Subsection: Filtering Excercise --  
	[MS Learn Article: Adding Filters to Reports](https://learn.microsoft.com/en-us/power-bi/create-reports/power-bi-report-add-filter?tabs=powerbi-desktop)

	We can filter our data to see only what we're interested in.
	
	The Filters pane displays along the right side of the report canvas. 	
	We can set filters at three different levels for the report.
		- The visual level.
		- The page level.	
		- The report level.

	Task: Create a new page called 'Product/Regional Sales'
		Quadrant 1 (1/4 page): 
			Make a clustered column chart of Product vs Sales (OR COPY/PASTE prev. bar chart)
		
		Quadrant 2 (1/4 page):
			Make a pie chart for Regional sales
			Suggestion: 	Turn on border for each slice.
				Make legend & labels bigger.
			
		Task: Filter by QUARTER (e.g. 1st Quarter)
			Options: 	Filter By Visual, Page, All Pages  
			Note: 	On the Filter Pane, when you apply a Filter you'll see # of rows returned on the right.
		
			NOTE: 
				The end user may not immediately see that a filter is applied.	
				To verify if there's a filter on a visual, 
				hover over the filter icon on a specific charts <b>Visual Headers</b> to see active filters.
				- We can create a "Clear All" Filters button, which we'll touch base on later. 

				
		For the Product Sales visual, filtering by one product (e.g., Laptops) show the bar chart containing only one product as a single bar.
		Similarly, if you filter the Regional Sales pie chart by one region, 
		then the pie becomes a full circle displaying only 1 region since all other regions are filtered out.

		One common use for filters: To exclude blank or empty values so they don’t clutter your report or distort results.
		Example: Using the table visual to filter out blanks.
		

	Task: Additional Filters
		- Filter Product Sales chart to show only products that generated over $1000000

		- FILTER TOP N
			Top 3 items By Value: (Field goes Here) Sum of Total Sales
	

-- Subsection: Slicers Excercise --

	The slicer visualization can be used to filter the other visuals on the page. 
	
	Quadrant 3 (1/4 page) On the same 'Product/Regional Sales' page: 
	Task: Create a slicer for Region & make it a tile.

		Change text of headers to make it big!:  			Visual -> Values -> Font Size
		Enable - SELECT ALL option:					Visual -> Slicer Settings -> Selection -> Show "Select All" As an Option
		Add a search box to the slicer to filter values by searching:	Click the three dots on the slicer’s visual header, select Search, and the search box will appear in the slicer.
			[Solution](https://community.fabric.microsoft.com/t5/Desktop/Slicer-Search-Bar/td-p/3010479)
		Change Slicer Type style options from 'Vertical List' to 'Tile': 	Visual -> Slicer Settings -> Option -> Tile
			Additionally we can make the font for "Values" to be bigger.
		

		Sync Slicers -> Slicers can be modified to affect other pages. To do so:
			First select the slicer
			Go to View -> Sync Slicers
				Make sure it's syncing for the current page & the page you want to affect.
	
			Note:
			It’s a good best practice to clear all filters first before deleting synced slicers.
 			Otherwise, it can be annoying/difficult to remove its effect from the other charts.


-- Subsection: Bookmarks --  
	[MS Article about Bookmarks](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-bookmarks)  
	[Video: Use bookmarks to change chart or visual with Button Click](https://youtu.be/EMfqGiFr6Y4?si=UGZle2pfMQKZmiJw)

	Bookmarks work are similar to MS Word bookmarks; Think of them as snapshots of your report you can quickly revisit or share.

	Bookmarks save the current state of a report(including filters, slicers, and visuals) so that you can:
		- Return to that view anytime.
		- Navigate between pages or sections.
		- Make interactive reports with clickable buttons or images.
				
		Task: Make a simple bookmark for the 'Product/Regional Sales' page
			
			Note: First assure that we are on the 'Product/Regional Sales' page.
			Enable bookmarks pane via View tab -> Bookmarks
			From the Bookmarks pane, select 'Add' to add a bookmark.
			Test: If we go to a different page and click that bookmark, it will take us to the saved page.
		
		Task: Create a bookmark that filters Quarter
			Remember: Bookmarks saves other settings too like filters, etc.


-- Subsection: Buttons --

	Recall:
	Visuals - Visualizations of semantic model data.
	Elements - Provide visual interest but don't use semantic model data. 
		Elements include text boxes, buttons, shapes, and images.


	Task: On a new page, add the following buttons under Insert -> Buttons:
		- Back Button (Once placed on canvas, Press Ctrl + Click to activate)
		- Page navigation! (Just like in PowerPoint)
			First create a page named "Home" or "Main Hub".
			Create button (e.g. a Circle shape) 
			Under the Shape tab in the Visual Pane, set Action -> Type -> Navigation, and link it to the previously created pages
			'Products/Region' and 'Products/Quarter'."
		- Bookmark Button
			- Under Button (Visual Pane Tab) -> Action -> 
				Type = "Bookmark" & BookMark = "Page 1" 
		- Insert a PANDA pic & add a link to the LA ZOO via "lazoo.org"
			Q: Does the 'panda' link work when you export to PDF?
			A: NO!!
		- Information Button
			- Add a Tool Tip [Under Visual Pane -> Button -> Actions -> Tooltip]
				Add text: "Please make sure to see the pages for the ENTIRE report"
			- Set it so nothing happens if the user accidently clicks it by mistake:
				Button (Visual Pane Tab) -> Actions -> Type = "Bookmark" & BookMark = "None" 
			- Give your tooltip a background color so people see easily via 
				Visual Pane -> Button -> Button -> Style -> Fill <OR> Style -> Glow 
				OR 
				General -> Effects -> Background
		- Optional: Create a button that's clears all slicers
			Remember: To activate the effect, we must Ctrl + Click the button.
		- Optional: A button on the report page could have the text 'Reset slicers', and when invoked, it uses the bookmark.
		Additional Info on Bookmark Buttons Settings:
			https://www.youtube.com/watch?v=rgKtgQhPPrg
			Data -> Reset data
			Display -> Spotlight, Showing/Highlighting
			Current Page -> Deselecting means we don't jump to that page, but that those settings are applied.
		- Q&A
		If a page contains data, 
		we can have Q&A access that data by going to said page and without selecting anything, click
		the Visual Pane -> "Format Your Page" -> Page Information -> Allow Q & A

		Sample Q's to ask:
			- count products
			- what are all the salespeople?
			- what are all the regions?
			- what are total sales / Get overall sales

		After we have our Q&A result, 	
		click on the "Turn this Q&A result into a standard visual" at the top right of visual to turn it into a standard visual 

		Q:	You added the Q&A feature to let users find answers on their own. 
			Which two configurations can you add to improve the search capabilities for them[end users]?"
		A:	- Add a linguistic relationship schema to the dataset.
				A linguistic schema describes terms and phrases that Q&A should understand for objects within a dataset, 
				including parts of speech, synonyms, and phrasings that relate to that dataset.
			- Add synonyms to model fields will help users search for them. 
				For example, you can give a synonym of (Actuals) for the (Sales) measure. 


-- Subsection: Groups --  
	[MS Article explaining Groups](https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-grouping-and-binning)
	
	When Power BI Desktop creates visuals, 
	it aggregates or groups your data into chunks based on the values it finds.
	Usually this is fine, but sometimes you may want to control how the data is grouped. 
	Like Excel PivotTables, you can group columns in Power BI which makes large charts or histograms that have many columns easier to read.


	Situation: 	Confirm there is a Quarterly Sales column chart showing 'Total sales' by 'Quarter'.
	Task: 		Form 2 groups: 1st half of year vs 2nd half of year.
	Action: 	
			On the far right data pane, right click on the field "Quarter" -> New Group
		
			On the pop up, name the group "First Half / Second Half"
			Now under 'Ungrouped Values' section -> 
				Using Ctrl+Select, select the elements "Quarter 1" & "Quarter 2" & then press "Group". Double click to rename the group to "H1"
				Using Ctrl+Select, select the elements "Quarter 3" & "Quarter 4" & then press "Group". Double click to rename the group to "H2"
			Press "Ok"
	Result: The group is created against a numerical column using bins.
		Create a bar chart that maps out "Total Sales" vs. group "First Half / Second Half"
		Note: The Bin group type is an auto grouping of items into bucketed bins (groups).


-- Subsection: Drill Down --  
	[MS Article Reference](https://learn.microsoft.com/en-us/training/modules/configure-semantic-model-power-bi/5-hierarchies)  
	[Test Your Knowledge](https://learn.microsoft.com/en-us/training/modules/configure-semantic-model-power-bi/9-check)


	We've covered interactions and highlights but to recap:
	Up to this point, when we create a chart and we click on it, it creates a highlight. 
	That highlight stands out from other elements within the chart or a cross-highlight/affect other charts as an interaction.
		
	With most datasets however, there are usually complex groups or subsets of data. 
	To manage this, we can create a hierarchy that by default gives the user a high-level overview of your data, 
		and it can drill down into more detailed levels as needed.
	i.e. Hierarchy = GROUPING/AGGREGATE

	Microsoft article: "Levels of a hierarchy are always based on columns from the same model table"
	In short: we're grouping a set of related fields together under a hierarchy.
		Whole Point: Improves organization & no need to make potential duplicate charts thereby saving space.
		

	
		
	Quadrant 1 (Use Focus Mode so that size of the chart doesn't matter):
	Scenario: We'll create a hierarchy of sales for 'Region' -> 'State' 

	Task: Create a Regional Sales Clustered Column Chart.
		Goal/Main idea: 
		Effectively we're creating two chart views; users can drill down and break the sales down by region and state. 
		Think: Default/Parent vs Detailed/Child View (I'll refer to it as parent and child level.)
			NOTE: If we had a ZIP field, we could break it down further to Region -> state -> Zip (if provided)
		
	Action:
		Step 1: Create a hierarchy on our Visual.
			In the X-Axis, add "State" field from Data Pane by dragging it underneath "Region" field.

		Result: Visual Headers (Similar to Excel Chart Tools) shows the drill down tools (to the left of the filter). 
			Clicking "Drill Up" shows the parent level.
			Clicking "Go to Next Level in the hierarchy" will show every states sales
			
	As a result, we've created a hierarchy with the point to save canvas space; 
	we use one chart to switch back and forth between all the regions and states, 
	instead of creating two separate charts.
		
	
	By default, clicking a region bar displays the table data for that region.
	
	Task: 	Turn this drilldown feature off by going to Data/Drill contextual tab, & deselect the option 'Data point table'
	Result: We've enabled drill-down mode so that clicking a bar no longer shows a table or standard highlight.
	
	Task: 	Enable Drill Down Mode to expand regional sales:
		2 ways:
			1st way: Click "Enable drill down" in the Chart tools
			2nd way: Select Chart -> Data/Drill Tab -> Drill Actions Group -> Drill Down Button
	
			
	Student Q: 	What if a user doesn't know that there's a DRILL DOWN??
	Answer:		We can add an INFORMATION SHAPE via Insert -> Buttons -> Information to notify them.


	- (Optional More practice) -
	Optional Excercise #1:
		Create a Quarter Sales chart.
		Enable drill-down on the X-axis to go from Quarter -> Order Date[Month] -> Order Date[Day].
		(This can be done by expanding Order date field) 
		
		Solution: 	
			Top level: Sales by Year
			Drill down: Sales by Order Month (within that year)
			Drill down again: Sales by Order Day (within that month)

			- x axis -
			Quarter
			Order Date
			  Month
			  Day
	
	Optional Excercise #2:
		In the last example with the 2 groups we created (1st half of year & 2nd half of year),
		place it at the highest level above Quarter.
 

	Recap: Understand:
		- interactivity
			- cross highlight - 	Click on the bar item to highlight all charts.
						Click outside the bar (but not outside the entire chart) to undo all.
		- filters 
			- moving an area to filters pane will allow you to filter (similar to PivotCharts!)
		- add slicers - just like how it's done in PivotCharts.
		- understand hierarchys & drill down.	


	Q: You need to create a new hierarchy in Power BI Desktop.
	What should you do first?

	A: To create a new hierarchy in Power BI Desktop, you must select Create hierarchy from the Model view or Report view. 
	NO DRAG/DROP!


/* -------------------------------------------------------
## <p id = "6"> Lesson 6: Enhancing Data Analysis | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */

[Reference Link](https://learn.microsoft.com/en-us/training/modules/power-bi-effective-reports/)

In this chapter, we will discuss more about charts & chart options.

As you know, Tooltips are pop ups that display extra details about a data point in a visual when you hover over it. 


		Under Sales Data, date categories are commonly mapped out via 
			Line Charts, Area Charts, Column Charts

		When we hover over the chart, we will see tooltip.

 		Let's say we want to compare quantity with total sales
		Sales is in millions, quantity is in thousands.
		We can do a compbo chart but make sure quantity is mapped in column legend


	
-- Fun Activity: Custom Tooltip Based on Report Pages --  
[Example of creating a chart as a tooltip](https://www.youtube.com/watch?v=cGpBUJpFWrM)

	By default, Tooltips show the value and category, but they can be customized to include more information.
		We can enhance tooltips by embedding full visuals from a separate report page. 
		These visuals, such as cards, gauges, or charts, are filtered based on the data point being hovered over, adding context to the main visual.

	Q: WHY ADD A CUSTOM TOOLTIP WHEN A DEFAULT ONE IS AlREADY ON THE CHART?
		A: Save space & change the default tooltip!

		
		Task: Use the 'Shape Maps' visual to map out State (Location) vs Total sales (Color Saturation)
		
		Why we only see the Map Tooltip page under the Page dropdown? Why we can't see other pages?
		
		? MUST FIRST BE ENABLED TO MIGHT NEED TO MAP TOOLTIP
		FYI: You might need to enable:
		https://community.fabric.microsoft.com/t5/Desktop/Map-and-filled-map-visuals-are-disabled/td-p/3116218


		Steps:			
		1. Create a new page & name it "Map-Tooltip". This will be our tooltip page.
		2. Under Visualizations side bar -> Format your report page -> 
			- Page Information -> Check off "Allow Use as tooltip"
			- Canvas Settings -> Type should be set to "Tooltip"
		3. 	We need to add the visuals to include in our tooltip.
			On a new page, let's create a simple clustered column chart
			(Optional) Add a pie chart of quarterly sales (or a card)
			(Optional) WE CAN ADD A CARD FOR STATE NAME
		
		Let's now assign a report page tooltip to a field in a visual:
		4. Go back to map, click on the map chart, and then go to Format Visualizations -> General Turn on tooltips -> 
				Type -> Report Page
				Page -> "Razatooltips"


	Real Life Example:
	Healthcare by state, showing regions that are most developed vs. those needing improvement

	ANOTHER EXAMPLE:
		Add a bar chart for product sales 
			Create a tooltip for quarterly sales so when we hover over a bar (e.g. laptops)
			we see just Laptops sales for each quarter.		


	
-- Extra Visuals / Extra time --  
	[Analyze Visuals](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-analyze-visuals)

	Create a a line graph that maps Monthly total sales.

		Do a filter for Q2
			let's analyze the top point by right clicking on the point -> Analyze !!!!


	- Add a Matrix visual if needed.
			'Matrix' visual is similar to Excel Pivot Table; 
				best when you need to show data with categories broken down into subcategories
			'Table' visual is similar to Excel Table; 	
				Best for showing raw, detailed data in a simple list, like a simple transaction log.
				i.e. no hierarchy! Just raw data.
				For your visual, make sure that when you place the field in the Fields pane → Columns area,
				that the dropdown for the added field (e.g. Product/State field) shows "Don’t summarize"
					- If the table doesn’t update, click outside the field or make a small change on the table.



	Key Influencers		
		identifies biggest factors influencing a metric
		factors that drive a particular metric (like sales).

		Analyze: Total Sales
		Explain By: Products

		“High sales are strongly influenced by the Laptops, Video Game & Camera category.”
		i.e. Key Products that affect sales are: Laptops, Video Games & Cameras

		Analyze: Salesperson
		Explain By: Region	

		Q? Which native AI visual helps explain correlations for a metric within the dataset?
		A: The Key influencers visual helps you understand correlated factors impacting a particular metric.


	Tree map	- Do 2 fields for PRODUCT & FOR QUARTER!
		A treemap visualization displays data as a set of nested rectangles.


	ARCGIS in POWERBI????


	Create a new page.
	Create a gage chart showing Total Sales & STATE for POWERBI!	
		 A gauge visual displays a circular arc including a single value that measures progress toward a goal or target.

		By default it shows a number, let's change this to State abbreviation
			Format Visual -> Visual -> Custom Label (ON) -> and then click on "+Add Data" to add the state.
		When we create a gauge, it is always at the half-way mark. How do we change that?
			
		Talk about targets & how a calculated column can be just that!
	
	Create a multirow card.
		We can increase the text size if we'd like..

	Decomposition Tree
		This visual lets you visualize data between multiple dimensions and drill down in any order.
		Analyze Total Sales
		Explain By:	
			Quarter
			Then by Region
		Visual Pane -> Under Category Labels -> Change Font Size.
	

	The Smart Narrative visual lets you combine natural language text with metrics from your model in sentence forms.


	You need to create a custom Python visual by using Power BI Desktop.
	What do you need to do first?
		To create a Python visual by using Power BI Desktop, you first need to install Python on your computer. 
		Once Python is installed, you may need configure the global Python scripting options in Power BI Desktop. 
		Enabling the script visuals option in the Visualization pane of Power BI Desktop is done once Python is installed. 
		Creating a custom Python visual by using Power BI Desktop has no dependency on enabling preview features.

	----
	Read more about [Performance Analyzer](https://learn.microsoft.com/en-us/training/modules/optimize-model-power-bi/2-performance)


=== Break ==

/* -------------------------------------------------------
## <p id = "7"> Lesson 7: Data Modeling w/Calculated Columns & Measures | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */


-- Subsection: Calculated Columns --  
	In Power BI, a calculated column is a new column that you create using a formula.  
	This new column:  
		- is a custom field that was created by using DAX  
		- calculates a value for every row in that table.  
		- this custom field doesn't come from the raw data source & we can use it in visuals, filters, or slicers just like any other field.  
	Note: To create a formula in Power BI (Calculated Column):  
		Option 1: In Power Query, use Custom Column  
		Option 2: In Table View within Power BI, click New Column to add it directly in the data model.  
		⚠️ Note: Columns created in Table View will not appear in Power Query.  
			Power Query is mainly for initial data transformations i.e. Power Query runs before the data is loaded into the model.
	
	Task: Create simple text calculated columns.
	Go to Table View (You can also make a calculated column in Report View, but Table View shows results)
	3 ways to create a new column:
		Tables Tools (Contextual Tab) -> New Column 
		OR
		Home Tab -> New Column 
		OR
		In the data pane, right clicking the table name -> New Column
 

		- Task: Create a static calculated column w/ the same value (“Hello World!”) for every row.
			firstNewColumn = "Hello World"
			NOTICE: Calculated columns generate row-level values to all rows, so every row will show “Hello World!”
					
		Optional Task: Try changing the value of 'firstNewColumn' to "I love PowerBI"
		

		- Task: Use ROUND() function to create 'Rounded Total Sales' Column
			Under the same Table View, click New Column & enter the formula:
 				Rounded Total Sales = ROUND(SalesData[Total Sales], 0)
	
		Optional Task:
			- Create a column joining the region & state. Solution:  
				ConcatColumn = SalesData[Region] & "-" & SalesData[State]
			- Create a tax related column.


		- Task: 
			Create a 'Duration' column to calculate the difference between Ship Date and Order Date. Solution: 
				Duration = SalesData[Shipped Date] - SalesData[Order Date]
				Afterwards, go to Column Tools (Tab) and change column data type to WHOLE NUMBER	
			

		- Task:
			Create a "Duration-Status-Message" column. 
			Using an IF Statement, if the duration is <3 then the value is "acceptable" else it's "late". Solution: 
				Duration-Status-Message = IF(SalesData[Duration] < 3, "Acceptable", "Late")
				
		
			Subtask: Let's create a visual.		
			Create a bar chart that counts "Acceptable" & "late" 
				Drag the "Duration-Status-Message" field for BOTH X & Y Axis 
				Optional: Create 1 card that outputs the earlier Message measure, & another with the Count.


		Optional IF Task: 	NewColumn = IF(SalesData[Total Sales] > 1000, "Big Sale","Not Big Sale")		
	

	NOTE:
		Calculated columns are computed row by row
		Values are stored in the data model => memory being taken up => increase file size and slow refreshes for large tables
		Overall: Good but inefficient.
	 

-- Subsection: Measures --

	Measures are similar to formulas.
	
	- When used in a visual, Measures are calculated on the fly so they don’t consume extra storage.
	- Measures don't create new columns of values for each row (i.e. No per-row calculation) 
	- They operate on entire fields and only appear in the Fields pane; they show calculations only when used in visuals.
	Recap: You can create and name measures just like calculated columns, BUT no calculation occur UNTIL the measure is added to a visual.
		- For instance, Power BI can’t create relationships using measures - can only use columns. 
			- Although they exist in the semantic model, bogus results are returned when we attempt something.


	Situation: We use a measure when we need a summary value (like average, comission)				
	Task: Create a measure named "Commission". Solution:
 		Commission = SUM(SalesData[Total Sales]) * 0.02
			
		- After creating a measure, no new column is added so thus there's no new value added for each row.
		- The measure applies to the whole field and appears in the side pane, showing values only when used in visuals.
		
		TASK: Create a new page for Salespeople.
			Create a bar chart that maps out SalesPeople Total Sales
			Create a GAGE CHART out of Measure Commission
			(Optional) Create a card showing sales person name/sales
					

			Note: Measures are explicit. 
			If an axis is displaying "average" of sales, then we can't change the field to display "sum" in the pane field! 
			We'll have to change the formula.
			
	Recap:
		Measures:
			Calculated only when needed (mainly when you use them in a visual or report).
			Don't take up extra space in your data model.
			Measures are most efficient for larger data sets when calculations don’t need to be stored row by row.

		Calculated Columns:
			Stored in memory for every row in your table, increasing the size of your model.
			Always calculated, even if not used in your report.
				link two tables based on a calculated value,
			- Unlike a measure, a calculated column can be used in a slicer to filter on the report page.


-- Subsection: Display Folder --  
	In Power BI, a Display Folder is a way to organize fields (columns, measures, hierarchies) in the Fields pane 
	without changing the underlying data model.  
		Purpose: Makes the Fields pane cleaner and easier to navigate.  
		- It’s purely for presentation and usability, especially in large models.
		
	Task: Create a display folder named 'Calculated Columns' for each of the columns we made.
		Calcualted Columns
  		├─ 'firstNewColumn'
  		├─ 'Rounded Total Sales'
  		└─ 'Duration-Status-Message'

	Step 1: Go to the Model view
	Step 2: Select the desired measures or columns
	Step 3: In the Properties pane, in the 'Display folder' field, type the folder name & then press Enter. 
	
	
-- Additional Q's & Notes: --  

	-- 
	A measure is a named DAX formula that summarizes model data.
	whereas
	A parameter allows what-if scenarios or field selection	
	-- 

	You decide to remove unnecessary columns from your data model.
	What are two potential performance benefits of doing this? Each correct answer presents a complete solution.



	OPTIONAL EXCERCISE:
	From Power BI Desktop, you open a Power BI report that contains three pages named Main, Error Rate, and On-time Rate.
	You add a button to the Main page for navigation.
	
	You need to implement a solution that meets the following requirements:

	- The navigation destination must change based on the output of a DAX measure named [Error Rate].
	- If [Error Rate] is greater than 5%, the button must display the text “Error Rate” and navigate to the Error Rate page.
	- Otherwise, the button must display the text “On-time Rate” and navigate to the On-Time Rate page.

	What three actions should you perform? Each correct answer presents part of the solution.
	
	To configure a button for conditional page navigation, 
	- you need to create a DAX measure that outputs the correct destination page name. 
	- Then configure the button to use page navigation and use the newly created DAX measure to specify the navigation destination. 
	- To change the button text to match the page name, conditional formatting must be used to set the text to equal the newly created DAX measure.
	Wrong: No bookmarks are necessary.
	It is not necessary to set the destination to a specific page since conditional formatting is used to specify the destination.
	

/* -------------------------------------------------------
## <p id = "7"> Lesson 8: Sharing & POWERBI SERVICE (PowerBI Online) | [Back to ToC](#toc)</p> 
---------------------------------------------------------- */

Links:  
	[Power BI Service Link #1](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-experience)  
	[Power BI service Link #2](https://learn.microsoft.com/en-us/training/modules/manage-workspaces-power-bi-service/)


Recall:
	Power BI Desktop for creating semantic models and reports with visualizations.
	Power BI service for creating dashboards from published reports and distributing content with apps
		

In a standard Power BI workflow, usually we:
	1. Create a report in Power BI Desktop 
	2. Publish it to the Power BI service.
Note: When we upload work from Desktop -> Online, the Desktop changes won’t change the online version unless you re-publish via Home -> Publish (Power BI Desktop)
For the web version, Reports are more like an online object rather than a traditional file.


	Task: 
		Go to app.powerbi.com (Make sure you are signed in).
		Notice: We can still use PB Service on a free tier account, albeit limited. 
		
	The Power BI service is composed of many building blocks, including workspaces, reports, semantic models, dashboards, and apps. 
	Each of these components play a unique role in the Power BI ecosystem.

-- Workspaces -- 

	Workspaces are the foundation of the Power BI service. 	

	Workspaces act like folders since it can organize: 
		semantic models, reports, and dashboards

	When publishing any report, you must choose a workspace:

		- Shared Workspaces are used to share content with others
		Shared Workspaces = team folders + permission system.
			We can assign roles (Admin, Member, Contributor, Viewer) to control access and editing.
			[Video discussing Workspace Roles](https://www.youtube.com/watch?v=L6urbTbrToo)		
		- By Default, "My Workspace" is a workspace every user has access to which is ideal only for testing. 

	Task: 	Once signed in, click on the icon "My Workspace" from the Navigation pane on the left hand side.

		"My workspace" is your personal folder/sandbox/area in Power BI for all your content and sample data.
			For instance, any sample data you download from the Power BI Learning Center is saved here.
			NOTE: With the free version of Power BI, "My Workspace" is the - ONLY! - workspace you can use in Power BI Service.
				
	From a workspace, we can open a dashboard or report by selecting it from the list. 
	Task: Upload a report to PowerBI Service 	


-- Dashboards --  
	Links:  
	- [Create dashboards in Power BI](https://learn.microsoft.com/en-us/training/modules/create-dashboards-power-bi/)  
	- [MS Article on Dashboards](https://learn.microsoft.com/en-us/power-bi/consumer/end-user-dashboards)

	Reports are built on a single dataset (semantic model) and can have multiple pages 
	A Dashboard is a single-page canvas designed for at-a-glance insights.
		- Dashboards can pin visuals from multiple reports/datasets, even from different semantic models onto 1 page.
			- You can only pin visuals to a dashboard; users can’t modify or create additional pages.
		- These pinned visuals that make up Dashboards are called Tiles.
			- Tiles highlight key metrics but they aren’t interactive like visuals; clicking a tile opens the underlying report.
	A dashboard is read-only — people can interact with tiles (like drilling through if enabled) but can’t edit visuals or add new visuals.
	Note: In the Power BI service, we create dashboards after we've published a report
	

	NOTE: Individual filters and slicers cannot be pinned to a dashboard. 
	The Pin visual option only allows you to pin the visual to an existing dashboard or create a new one. 
			

	Managers can share dashboards for users to view KPIs, 
	but creating custom reports requires build permission access to the underlying dataset. 
	In short, most users are viewers/consumers, not producers, unless granted dataset permissions.
		EX: 	If your manager shares a Sales Dashboard, you can view KPIs. 
			To build your own Sales report, you’ll need access to the underlying Sales Dataset.



-----------------
Subscriptions are scheduled email snapshots of reports/dashboards.  
Bonus Task: Make a subscription
-----------------


-----------------
Reports (unlike dashboards) can be embedded into a webpage

Reports, unlike dashboards, can be embedded into websites or applications using Publish to Web (for public access) 
or Power BI Embedded / Secure Embed (for authenticated users).

Bonus Task: Publish a Power BI report to the web using Power BI Service:

Step 1: Open Your Report in Power BI Service

	Sign in to Power BI Service
	Open the workspace that contains your report.
	Click on the report you want to publish.

Step 2: Use “Publish to Web”
	
	In the report view, click File -> Embed Report -> Publish to web.
	A dialog box will appear explaining that the report will be publicly accessible on the internet.
	⚠️ Important: Anyone with the link can view it. Do not use this for sensitive or private data.

Step 3: Get the Embed Code or Link
	Click Create embed code.
	You’ll get:
		Link: Shareable URL to the report.
		Embed code: HTML iframe code you can paste into a webpage.

Step 4: Add to Your Webpage
	Copy the iframe code.
	Paste it into your website’s HTML where you want the report to appear.

Notes / Limitations
- Only works with reports, not dashboards.
- The report will be public, no authentication required.
- Some organizations disable this feature for security reasons. If you don’t see “Publish to web,” check with your Power BI admin.
-----------------




	Q:
	You upload reports to the Power BI service and pin several visuals to a dashboard. You plan to create alerts rules for several visuals.
	What are two locations you can view the alerts? Each correct answer presents a complete solution. Select all answers that apply.

	- a report
	[x] - an email
	- Microsoft Teams
	[x] the Notification Center
	
	Explanation: By default, notifications are available in the notification center. You also have the option of sending notifications via email. 
	A dashboard, Microsoft Teams channel, and a report are not available as the locations of alerts.

	Q: You need to create a Power BI dashboard.
	Which tool should you use? Select only one answer.

	- Power BI Desktop
	- Power Query Editor
	- the Power BI mobile app
	[x] the Power BI service

	Explanation: 	The Power BI service provides support for creating Power BI dashboards. 	
			The Power BI mobile app can be used to view dashboards, but not to create them. 
			Power BI Desktop does not provide support for creating Power BI dashboards. 
			Power Query is a Microsoft Excel tool that is used for importing data, but not for creating dashboards.
	
	Q:You need to add a new visual to a Power BI Dashboard. This visual does NOT exist on a report in the workspace.
	What should you do first? Select only one answer.

	- Open See Related Content.
	- Open the File menu.
	- Select Add a tile.
	- Select Ask a question about your data.

	The Q&A feature lets you create a visual by typing in a question about your data. 
	This new visual can then be pinned to the dashboard, without adding it to a report.
	The Q&A visual allows end-users to ask natural language questions to create AI generated charts based on the questions.




===
Bonus Links:
	https://github.com/MicrosoftLearning/PL-300-Microsoft-Power-BI-Data-Analyst
	https://microsoftlearning.github.io/PL-300-Microsoft-Power-BI-Data-Analyst/
	https://www.reddit.com/r/PowerBI/comments/15js89a/guide_i_passed_the_two_official_power_bi/
	
	Bonus: Models:
	https://learn.microsoft.com/en-us/power-bi/transform-model/model-explorer