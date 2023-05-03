Download Link: https://assignmentchef.com/product/solved-cs1675-homework-1-ggplot2-and-dplyr-packages
<br>
This homework assignment focuses on the ggplot2 and dplyr packages. You will work with aesthetics and practice data manipulation operations. Additionally, you will practice working with R Markdown by completing the template. You can see what the rendered document looks like at any time, by pressing the “Knit” button within RStudio. You can execute a code chunk by pressing the arrow button within that code chunk located to the upper right portion of the code chunk within the RStudio IDE. Alternatively, you can execute a line of code within a code chunk by selecting that line and pressing Ctrl+ENTER (Windows) or Command+ENTER (Mac).

Completing this assignment requires filling in missing pieces of information from existing code chunks, programming complete code chunks from scratch, typing discussions about results, and working with LaTeX style math formulas. A template .Rmd file is available to use as a starting point for this homework assignment. The template is available on CourseWeb.

<strong>IMPORTANT:</strong> Please pay attention to the eval flag within the code chunk options. Code chunks with eval=FALSE will <strong>not</strong> be evaluated (executed) when you Knit the document. You <strong>must</strong> change the eval flag to be eval=TRUE. This was done so that you can Knit (and thus render) the document as you work on the assignment, without worrying about errors crashing the code in questions you have not started. Code chunks which require you to enter all of the required code do not set the eval flag. Thus, those specific code chunks use the default option of eval=TRUE.

<h2>Load packages</h2>

This homework assignment will use the following packages:

library(dplyr)library(ggplot2)

<h2>Problem 1</h2>

The supplemental reading material <a href="https://github.com/jyurko/CS_1675_Spring_2020/blob/master/week_01/quick_r_intro.md">A Very Quick Intro to R</a> introduced ggplot2 by creating a histogram for the Sepal.Length variable within the iris dataset. We will use that figure to practice modifying color within a ggplot2 graphic.

<h3>1a)</h3>

<h4>PROBLEM</h4>

<strong>Create a histogram for </strong><strong>Sepal.Length</strong><strong> from </strong><strong>iris</strong><strong> with 6 bins, instead of the 15 bins used within the supplemental reading material.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>1b)</h3>

By default, a ggplot2 histogram does not show the lines associated with each bin (as in a bar graph). The histogram effectively looks like a discretized distribution. To adjust this, we need to override the default fill and color arguments to the geom_histogram() function. Note that within ggplot2, color is applied to line-like objects and points while fill is applied to whole areas of the graph (think “fill in an area”). Thus, you can have substantial control over how color is used to visually present information within a graphic.

Even though an aesthetic can be linked to a variable, some aesthetics can be modified “manually” and not associated with any variables within the dataset. We use the same type of argument, but we set that argument outside of the aes() function.

<h4>PROBLEM</h4>

<strong>To see how this works, type </strong><strong>color = “black”</strong><strong> within the </strong><strong>geom_histogram()</strong><strong> call. Be careful about your commas!</strong>

<h4>SOLUTION</h4>

### your code here

<h3>1c)</h3>

ggplot2 has many “named” colors available for use. If you really want to fine tune your colors you are free to use the hex color codes! In this course, we will typically stick with common colors when we manually pick a color and/or fill.

<h4>PROBLEM</h4>

<strong>To make the difference between color and fill explicit within the histogram, change the color to </strong><strong>color = “navyblue”</strong><strong> and modify the histogram’s fill by setting </strong><strong>fill = “gold”</strong><strong>.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>1d)</h3>

We can alter the size or thickness of the lines around each bin with the size argument.

<h4>PROBLEM</h4>

<strong>Set </strong><strong>size = 1.55</strong><strong> within the </strong><strong>geom_histogram()</strong><strong> call (using the same color scheme from Problem 1c)).</strong>

<h4>SOLUTION</h4>

### your code here

<h3>1e)</h3>

Lastly, the transparency of geometric objects can be altered with the alpha argument.

<h4>PROBLEM</h4>

<strong>Set the transparency to </strong><strong>alpha = 0.5</strong><strong> within the </strong><strong>geom_histogram()</strong><strong> call.</strong>

<h4>SOLUTION</h4>

### your code here

<h2>Problem 2</h2>

As discussed in the supplemental reading material, geom_histogram() performs multiple operations behind the scenes in order to generate the histogram visualization. Understanding how those operations work will provide useful data wrangling and manipulation practice.

<h3>2a)</h3>

ggplot2 takes care of the binning and counting operations for us when we call the histogram function. Thus, we must perform those steps in order to recreate the histogram “from scratch”. We will start by learning how to discretize a continuous variable. To accomplish this, we will need to create a vector which defines the edges of each bin within the histogram. Within R nomenclature, the edges are referred to as “breaks”.

<h4>PROBLEM</h4>

<strong>Since we used 6 bins for our histogram, how many breaks are associated with the histogram? Assign your answer to the variable </strong><strong>num_breaks</strong><strong> in the code chunk below.</strong>

<h4>SOLUTION</h4>

num_breaks &lt;- ### your answer here

<h3>2b)</h3>

Next, create the vector hist_breaks by breaking up the range spanned by Sepal.Length via the seq() function. seq() has two main arguments: from and to. As the names suggest, the from argument is the start of the vector and the to argument is the end of the vector. In this problem, we will set the from and to arguments such that all observations are within the assigned discretized bounds. The third argument to seq() can take multiple forms, but all serve the same purpose: to define the length of the vector. For this problem, we will use the length.out argument.

<h4>PROBLEM</h4>

<strong>Create the vector </strong><strong>hist_breaks</strong><strong> with the </strong><strong>seq()</strong><strong> function. Use the provided </strong><strong>lower_bound</strong><strong> and </strong><strong>upper_bound</strong><strong> values in the code chunk below as the </strong><strong>from</strong><strong> and </strong><strong>to</strong><strong> arguments, respectively. Specify the </strong><strong>length.out</strong><strong> argument to be equal to </strong><strong>num_breaks</strong><strong>.</strong>

<h4>SOLUTION</h4>

lower_bound &lt;- 4.2 upper_bound &lt;- 8.2 hist_breaks &lt;- seq(from = , to =, length.out = num_breaks)

<h3>2c)</h3>

With the break positions defined, we can discretize Sepal.Length into bins via the cut() function. To learn about cut(), type ?cut into the R console in order to bring up the documentation. As the help page says, cut() divides a numeric variable into discrete bins and converts the result the a factor. The bin “edges” are based on the values specified by the breaks argument to the cut() function. We will practice working with cut() first, before applying it to the Sepal.Length variable within the iris dataset.

<h4>PROBLEM</h4>

<strong>In the code chunk below, assign the sequential integers </strong><strong>0</strong><strong> through </strong><strong>11</strong><strong> to the variable </strong><strong>x_dbl</strong><strong> using the </strong><strong>:</strong><strong> notation. Then pass </strong><strong>x_dbl</strong><strong> to the </strong><strong>cut()</strong><strong> function and specify the breaks to be 0, 5, and 11 by creating a vector containing just those three values. Assign the result of the </strong><strong>cut()</strong><strong> function to the variable </strong><strong>x_factor</strong><strong>. Check the data type associated with </strong><strong>x_factor</strong><strong>, and then print the </strong><strong>x_factor</strong><strong> variable to the screen.</strong>

<h4>SOLUTION</h4>

x_dbl &lt;- ### create vector 0 to 11 x_factor &lt;- cut(x_dbl, breaks = ) ### set the breaks argument class(x_factor) x_factor

<h3>2d)</h3>

The unique values associated with a factor variable are displayed in the line below the individual elements of the vector. In R nomenclature, factor unique values are referred to as “levels”. In your answer to Problem 2c) however, you should notice that the first printed element reads &lt;NA&gt;. That’s because the discretized intervals are setup to be (, ] (which reads as “from but exluding lower value, to and including upper value”). We can modify this structure to include the lowest (minimum) value in the dataset by setting include.lowest = TRUE in the call to the cut() function.

<h4>PROBLEM</h4>

<strong>Reperform the </strong><strong>cut()</strong><strong> call on </strong><strong>x_dbl</strong><strong>, but this time set </strong><strong>include.lowest = TRUE</strong><strong>. Assign the result to the vector </strong><strong>x_factor_2</strong><strong> and then print the result to the screen.</strong>

<h4>SOLUTION</h4>

x_factor_2 &lt;- cut(x_dbl, breaks = ) ### set the breaks and add the new argument x_factor_2

<h3>2e)</h3>

We will now modify the iris dataset by discretizing Sepal.Length via the cut() function. We will use the dplyr::mutate() “action verb” to execute this task. As the function name suggests, mutate() modifies the dataset by creating new variables. The generic syntax is mutate(&lt;new variable&gt; = &lt;set of actions&gt;). We can perform simple actions to create a new variable, or execute a complex set of tasks. dplyr::mutate() is a general “wrapper” for performing those operations.

<h4>PROBLEM</h4>

<strong>Create the new discretized variable, </strong><strong>sepal_length_bin</strong><strong>, by setting the </strong><strong>breaks</strong><strong> argument within the cut function to be </strong><strong>hist_breaks</strong><strong> and set the </strong><strong>include.lowest</strong><strong> argument to be </strong><strong>TRUE</strong><strong>. Assign the modified dataset to the variable </strong><strong>my_iris</strong><strong>.</strong>

<h4>SOLUTION</h4>

my_iris &lt;- iris %&gt;%   mutate(sepal_length_bin = )

<h2>Problem 3</h2>

Our new dataset, my_iris, contains an additional variable compared to the “base” iris. We will now practice manipulating the dataset based on grouping with this new variable.

<h3>3a)</h3>

Let’s get an overview of the newly created variable, sepal_length_bin.

<h4>PROBLEM</h4>

<strong>Use the </strong><strong>select()</strong><strong> action verb to isolate the </strong><strong>sepal_length_bin</strong><strong> variable from the other variables and pipe the result to the </strong><strong>summary()</strong><strong> function.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>3b)</h3>

Because sepal_length_bin is a factor variable, we can easily get the unique values (levels) with the levels() function.

<h4>PROBLEM</h4>

<strong>Pass the </strong><strong>sepal_length_bin</strong><strong> vector into the </strong><strong>levels()</strong><strong> function, by accessing it with the </strong><strong>$</strong><strong> operator from within </strong><strong>my_iris</strong><strong>.</strong>

<h4>SOLUTION</h4>

levels( )

<h3>3c)</h3>

In general, we can use the unique() function to identify the unique values contained within a vector irregardless of whether that vector is a “numeric”, “character”, or a factor variable. There are several important differences between factor levels and unique values, but we will not be too concerned with those differences at the moment.

<h4>PROBLEM</h4>

<strong>Call </strong><strong>unique()</strong><strong> on </strong><strong>sepal_length_bin</strong><strong> by accessing the variable with the </strong><strong>$</strong><strong> operator again.</strong>

<h4>SOLUTION</h4>

unique( )

<h3>3d)</h3>

As you should have seen in the previous set of results, the levels() and unique() functions return vectors. However, if we use the dplyr function distinct(), we will return a data.frame containing the unique values associated with the variable(s). We tell distinct which variable(s) to focus on using non-standard evaluation.

<h4>PROBLEM</h4>

<strong>In the code chunk below, pipe </strong><strong>my_iris</strong><strong> to the </strong><strong>distinct()</strong><strong> function and specify the variable to be </strong><strong>sepal_length_bin</strong><strong>.</strong>

<h4>SOLUTION</h4>

my_iris %&gt;%   distinct()

<h3>3e)</h3>

distinct() is a useful function, but it does not provide any other information about the variables. The count() function, however, returns the number of rows asssociated with each unique value. The number of rows (or the count) are stored in an automatically created additional column named n.

<h4>PROBLEM</h4>

<strong>In the code chunk below, apply the </strong><strong>count()</strong><strong> function instead of the </strong><strong>distinct()</strong><strong> function to the </strong><strong>sepal_length_bin</strong><strong> variable.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>3f)</h3>

We have sufficient information with the count() function result to make a bar graph in the style of the histogram we are interested in.

<h4>PROBLEM</h4>

<strong>Pipe the result of the </strong><strong>count()</strong><strong> function into the </strong><strong>ggplot()</strong><strong> function. Set the </strong><strong>x</strong><strong> and </strong><strong>y</strong><strong> aesthetics to be </strong><strong>sepal_length_bin</strong><strong> and </strong><strong>n</strong><strong>, respectively. Then call </strong><strong>geom_bar()</strong><strong>. However, by default </strong><strong>geom_bar()</strong><strong> will not work with this setup. As with </strong><strong>geom_histogram()</strong><strong>, </strong><strong>geom_bar()</strong><strong> performs a grouping and counting operations behind the scenes. To override this default behavior, we must modify the </strong><strong>stat</strong><strong> argument to be </strong><strong>stat = “identity”</strong><strong>. The code chunk below already has the correct </strong><strong>geom_bar()</strong><strong> call. Fill in the missing code to create the visualization of interest.</strong>

<h4>SOLUTION</h4>

### complete the ggplot call belowmy_iris %&gt;%   count(sepal_length_bin) %&gt;%   ggplot(mapping = aes( )) +  geom_bar(stat = “identity”)

<h3>3g)</h3>

The resulting bar graph in Problem 3f) looks different from the histogram visualized in Problem 1).

<h4>PROBLEM</h4>

<strong>Why is the x-axis setup differently from the histogram in Problem 1)?</strong>

<h4>SOLUTION</h4>

Type your answer here.

<h2>Problem 4</h2>

The count() function is useful for quickly grouping and counting by one or multiple variables. However, that is all the function is intended to do. In order to perform other calculations we need to use the group_by() function in conjunction with a function like summarize(). In this problem, you will learn about these very useful and important operations.

<h3>4a)</h3>

The grouping variables are specified using non-standard evaluation in the group_by() call. Thus, to group by a variable use the following syntax: group_by(&lt;variable name&gt;). Grouping by 3 variables is just a straight forward extension of this: group_by(&lt;variable 1&gt;, &lt;variable 2&gt;, &lt;variable 3&gt;).

<h4>PROBLEM</h4>

<strong>Pipe </strong><strong>my_iris</strong><strong> into the </strong><strong>group_by()</strong><strong> function and specify the grouping variable to be </strong><strong>sepal_length_bin</strong><strong>.</strong>

<h4>SOLUTION</h4>

my_iris %&gt;%   group_by( )

<h3>4b)</h3>

The result after applying the grouping operation appears to be just the original dataset. However, this new dataset “knows” the grouping structure. Thus, any additional operations we apply will be applied to the grouped dataset. When we wish to summarize based on the grouping structure, we pipe the group_by() result into the summarize() function. Calculations within the summarize() function are performed with syntax like we used with the mutate() function.

The code chunk below shows how the number of observations per sepal_length_bin value are computed using the n() function within the summarize() call.

<h4>PROBLEM</h4>

<strong>Complete the code chunk below by naming this summary variable </strong><strong>num_obs</strong><strong>. How do the resulting counts compare with the result from </strong><strong>count()</strong><strong>?</strong>

<em>Note</em>: the n() function is an example of a function without any input arguments. The syntax for calling such a function still requires the () after the function name. This syntax instructs the R interpreter that you are using a function named n and not a variable named n.

<h4>SOLUTION</h4>

my_iris %&gt;%   group_by( ) %&gt;%   summarise(  = n())

Type your answer to the question here.

<h3>4c)</h3>

We can do more than just counting in the summarize() call. We can calculate averages, standard deviations, quantiles, and even call complex modeling functions. Think of summarize() as a versatile wrapper function for controlling operations applied to a grouped dataset.

<h4>PROBLEM</h4>

<strong>Complete the code chunk below to calculate the average, minimum, and maximum </strong><strong>Sepal.Length</strong><strong> values for each </strong><strong>sepal_length_bin</strong><strong> level. In </strong><strong>R</strong><strong>, the average is calculated with the </strong><strong>mean()</strong><strong> function. The minimum and maximum values are calculated with the </strong><strong>min()</strong><strong> and </strong><strong>max()</strong><strong> functions, respectively. The grouped and summarized dataset has been named </strong><strong>iris_group</strong><strong> and is printed to the screen for review.</strong>

<h4>SOLUTION</h4>

iris_group &lt;- my_iris %&gt;%   group_by( ) %&gt;%   summarise(num_obs = n(),            avg_sepal_length = ,            min_sepal_length = ,            max_sepal_length = ) iris_group

<h3>4d)</h3>

We can use the grouped and summarized dataset to create a simple histogram which introduces the geom_point() and geom_linerange() geoms. geom_point() creates a basic scatter plot between two variables mapped to the x and y aesthetics.

<h4>PROBLEM</h4>

<strong>In the code chunk below, assign </strong><strong>avg_sepal_length</strong><strong> to the </strong><strong>x</strong><strong> aesthetic within the parent </strong><strong>ggplot()</strong><strong> call. Then, set </strong><strong>num_obs</strong><strong> to the </strong><strong>y</strong><strong> aesthetic within the </strong><strong>geom_point()</strong><strong> call. Lastly, assign the </strong><strong>size</strong><strong> argument within </strong><strong>geom_point()</strong><strong> to be 4.</strong>

<h4>SOLUTION</h4>

iris_group %&gt;%   ggplot(mapping = aes(x = )) +  geom_point(mapping = aes(y = ),             size = )

<h3>4e)</h3>

A scatter plot can be very useful graphic, but it can be difficult to visualize the distribution shape we are trying to represent in this example. To aid in that visualization, we will add vertical lines to our graphic via the geom_linerange() function. In geom_linerange() we must specify an x aesthetic and two separate y-axis aesthetics, ymin and ymax. As their names suggest, ymin displays the minimum value on the y-axis and ymax shows the maximum value on the y-axis. geom_linerange() then draws a vertical line connecting the y-axis aesthetics. Since we want to use the vertical lines to represent a histogram, set ymin to be 0 and ymax to equal num_obs. Thus, a vertical line will provide a comparable visualization as the bar chart from Problem 3.

<h4>PROBLEM</h4>

<strong>Complete the code chunk below by correctly assigning the y-axis aesthetics.</strong>

<em>Note</em>: this style of figure is sometimes referred to as a stem plot. They are useful in certain contexts, but when creating histograms I prefer the default ggplot2 geom_histogram() or geom_freqpoly() style. We used the stem plot in this problem to introduce additional geoms and to continue demonstrating the group_by() and summarize() functions.

<h4>SOLUTION</h4>

iris_group %&gt;%   ggplot(mapping = aes(x = )) +  geom_linerange(mapping = aes(ymin = ,                               ymax = )) +  geom_point(mapping = aes(y = ),             size = )

<h3>4f)</h3>

Let’s now compare our manual histogram to ggplot’s histogram. Our stem plot simplified histogram visualized the counts at the average Sepal.Length value within each bin. geom_freqpoly() plots the counts at the bin midpoint. Thus, assuming the bin center and the (empirical) average within a bin are similar, we should have an “apples-to-apples” comparison between geom_freqpoly() and our stem plot.

The graphic we wish to make does not just contain multiple layers but multiple datasets! The reason why is because we have to allow geom_freqpoly() to operate on the original non-grouped and non-summarized dataset. We can override the data associated with a geom by supplying an alternative dataset to the data argument. In this way, we can create complex figures which make use of various datasets.

<h4>PROBLEM</h4>

<strong>Complete the code chunk below by setting the </strong><strong>data</strong><strong> argument to </strong><strong>geom_freqpoly()</strong><strong> to be </strong><strong>my_iris</strong><strong>. Specify the appropriate variable to the </strong><strong>x</strong><strong> aesthetic within the </strong><strong>geom_freqpoly()</strong><strong> call. Assess how well our manual histogram performed relative to the native ggplot histogram. Were we close? What are the differences?</strong>

<h4>SOLUTION</h4>

iris_group %&gt;%   ggplot(mapping = aes(x = )) +  geom_freqpoly(data = ,                mapping = aes(x = ),                bins = 6, color = “red”, size = 1.15) +  geom_linerange(mapping = aes(ymin = ,                               ymax = )) +  geom_point(mapping = aes(y = ),             size = )

Describe the differences between the two here.

<h2>Problem 5</h2>

So far, we have used several different types of geometric objects. In this problem, we will introduce another very important geom, the boxplot, which provides a quick visual display of useful summary statistics for continuous variables (“numeric”s). Compared with the histogram which focuses on displaying the <em>shape</em> of the distribution, the boxplot allows us to visually relate the median with the 25th and 75th quantiles, as well as outliers. We get an idea about the central tendency of the variable, as well as a rough guide on the “meaningful” range.

To demonstrate the usefulness of the boxplot, we will use the diamonds dataset from ggplot2.

<h3>5a)</h3>

<h4>PROBLEM</h4>

<strong>Pipe </strong><strong>diamonds</strong><strong> into the </strong><strong>glimpse()</strong><strong> function to display the dimensions and datatypes associated with the variables within the dataset.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>5b)</h3>

The variable price gives the cost of a diamond in US dollars, while the other variables provide attributes associated with a diamond. A natural question to ask then is: <em>What variables influence the price?</em> If you have purchased a diamond before, you may have heard about the “4 C’s”: cut, color, clarity, and carat. We will explore the behavior of price with respect to these 4 variables.

The first three of these are all factors (the “ord” data type is a special ordered factor which as the name states has a natural ordering of the categorical levels) within the diamonds dataset, while carat is a “numeric” variable. With a boxplot, we group a continuous variable based on a categorical variable, and display summary statistics associated with the continuous variable for each categorical level. Therefore, the boxplot geom is another geometric object which performs multiple operations behind the scenes. If you have not worked boxplots before, I recommend Chapter 7 of the <a href="https://r4ds.had.co.nz/">R for Data Science</a> book.

Let’s start by visualizing the relationship between price and color.

<h4>PROBLEM</h4>

<strong>Pipe </strong><strong>diamonds</strong><strong> into </strong><strong>ggplot()</strong><strong> and set the </strong><strong>x</strong><strong> and </strong><strong>y</strong><strong> aesthetics to </strong><strong>color</strong><strong> and </strong><strong>price</strong><strong>, respectively. Then, call </strong><strong>geom_boxplot()</strong><strong>. What conclusion would you draw based on the resulting figure?</strong>

<h4>SOLUTION</h4>

### your code here

Discuss your conclusions here.

<h3>5c)</h3>

Next, we will include the influence of the cut variable breaking up the graphic into separate subplots based on the levels of cut.

<h4>PROBLEM</h4>

<strong>Add the </strong><strong>facet_wrap()</strong><strong> call to the code from Problem 5b), and set the facetting variable to be </strong><strong>cut</strong><strong>.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>5d)</h3>

In addition to the facet_wrap() function, we can create subplots with the facet_grid() function. As the name suggests, facet_grid() creates a 2D grid layout where each subplot corresponds to a combination of two facetting variables. As with facet_wrap(), the syntax uses the formula interface: facet_grid(&lt;vertical variable&gt; ~ &lt;horizontal variable&gt;). The variable provided to the left of the ~ varies top-to-bottom (vertically), while the variable to the right of the ~ changes left-to-right (horizontally).

<h4>PROBLEM</h4>

<strong>To see how this works, use </strong><strong>facet_grid()</strong><strong> instead of </strong><strong>facet_wrap()</strong><strong> and set the facetting variables to be </strong><strong>clarity</strong><strong> and </strong><strong>cut</strong><strong> for the vertical and horizontal directions, respectively.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>5e)</h3>

The resulting figure in Problem 5d) includes 3 out of the 4 C’s. The remaining variable, carat, is not categorical. To include carat in our figure, let’s discretize it and compare two boxplots side-by-side at each color level within each clarity and cut subplot combination. For now, we will keep things simple and break up carat based on if an observation has a value greater than the median carat value.

<h4>PROBLEM</h4>

<strong>Within the </strong><strong>geom_boxplot()</strong><strong> function, set the </strong><strong>fill</strong><strong> aesthetic to be a conditional test: </strong><strong>carat &gt; median(carat)</strong><strong>. As shown in the supplemental reading material, use the </strong><strong>theme()</strong><strong> function to move the legend position to the top of the graphic.</strong>

<em>Note</em>: It might be difficult to see everything within the graphic window dispalyed in the result after the code chunk, when working within the .Rmd file in the RStudio IDE. You can zoom in by clicking on the “Show in New Window” icon which is displayed as the small “arrow over paper” icon to the right hand size of the output portion. Alternatively, the figure dimensions can be modified by the code chunk parameters fig.width and fig.height. <strong>For this assignment, it is ok to use the default figure dimensions.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>5f)</h3>

Due to the large number of subplots, the individual facets are quite small with the default figure size. Let’s focus on the case with cut == “Ideal” and clarity == “IF” by calling filter() before piping the dataset into the ggplot().

<h4>PROBLEM</h4>

<strong>Pipe </strong><strong>diamonds</strong><strong> into </strong><strong>filter()</strong><strong> and perform the necessary operation. Pipe the resulting dataset into the same </strong><strong>ggplot2</strong><strong> function calls used in Problem 5e), except for one important change. The </strong><strong>filter()</strong><strong> call will reduce the dataset, and thus our conditional test will be comparing </strong><strong>carat</strong><strong> to the median value associated with the smaller dataset. To force the conditional test to still be applied to the median based on the complete dataset use </strong><strong>median(diamonds$carat)</strong><strong> within the conditional test instead of </strong><strong>median(carat)</strong><strong>.</strong>

<h4>SOLUTION</h4>

### your code here

<h3>5g)</h3>

<h4>PROBLEM</h4>

<strong>Discuss the differences between the trends shown in the resulting figure in Problem 5f) with the trends shown in the figure in Problem 5b).</strong>

<h4>SOLUTION</h4>

Type your discussion here.

<h2>Problem 6</h2>

We can create LaTeX style math expressions within R Markdown. To get more comfortable writing these type of expressions, we will work examples similar to those discussed in the calculus review in the first week of lecture.

<h4>Quick introduction to LaTeX</h4>

In R Markdown, math notation and expressions can be displayed inline by typing expressions between dollar signs. For example, typing $x$ displays (x) in the rendered document. If we instead want to display a bold face variable (to represent a vector) we will need to include the LaTeX style function mathbf() between the dollar signs. Thus, typing $mathbf{x}$ renders (mathbf{x}) in the document.

LaTeX style expressions provide a lot of flexibility and enable us to write out expressions just like we would on paper. To show a subscript “attached” or “associated” with variable such as (x_1), you must use the underscore character _ next to that variable. Thus, type $x_1$ to display (x_1). If you have a relatively complicated expression you want to show within the subscript, you can wrap curly braces {} around the subscript expression. For example to display (x_{i,j,k,l}) simply type $x_{i,j,k,l}$.

Superscripts, such as (x^2), are displayed with the ^ operator. Thus, to show the square of the variable (x), type $x^2$. As with subscripts, you can wrap complicated expressions within curly braces. To show (x^{t+2}), type $x^{t+2}$. Subscripts and superscripts can also be combined together, such as with (x_{n}^{2}). When combining subscripts and superscripts, it’s recommended to wrap each expression within curly braces, even if the expression is simple. Therefore, to display (x_{n}^{2}), type $x_{n}^{2}$.

We can display variables and complete expressions within parentheses, such as (left(x+aright)), several different ways. First, you can simply type $(x + a)$ which produces ((x + a)). Another option though is to use the following commands $left( x + a right)$ which also produces (left( x + a right)). At first glance these seem to be the same, but the left( right) commands allow the parantheses to be dynamically sized around the expression they contain. For more information on different types of brackets and parantheses, please see the following reference from <a href="https://www.overleaf.com/learn/latex/Brackets_and_Parentheses">Overleaf</a>.

We can also display equations within “equation blocks” using two dollar signs to surround the expression of interest. The equation within the block is rendered beneath text in the rendered report. We can thus draw special focus to mathematical equations and expressions displayed this way.

As an example, consider a function of two variables, (x_1) and (x_2), shown in the equation block below:

[ fleft(x_1, x_2 right) = a x_{1}^{b} + c x_{2}^{d} ]

To create the above equation, type the following:

$$ fleft(x_1, x_2 right) = a x_{1}^{b} + c x_{2}^{d} $$

Reading the un-rendered LaTeX expression may seem daunting at first, and getting used to working with LaTeX math coding can be challenging. However, please note that the above expression combines each of the previously described elements together. Each individual element, such as a subscript or superscript is relatively straight forward. Thus, when starting out with LaTeX, break a complicated expression into separate components or elements. Get those elements correct, and then “assemble” them into the final expression of interest.

Let’s now get additional practice by working through the partial derivatives of the above function.

<h3>6a)</h3>

To write out the derivatives, we need to understand how to type fractions in LaTeX notation. A fraction consists of three parts. The first is the phrase frac. The remaining two parts of a fraction are two sets of curly braces. The complete syntax is frac{}{}. The numerator is typed within the first set of curly braces and the denominator is typed within the second set of curly braces. Thus, the formulation for a fraction is:

frac{&lt;numerator expression&gt;}{&lt;denominator expression&gt;}.

As an example, one half written as a fraction is $frac{1}{2}$. The rendered LaTeX expression looks like (frac{1}{2}).

<h4>PROBLEM</h4>

<strong>Write out the partial derivative of </strong><strong>(f)</strong><strong> with respect to </strong><strong>(x_1)</strong><strong>. To receive full credit you must use the </strong><strong>frac{}{}</strong><strong> to write out the partial derivative of </strong><strong>(f)</strong><strong> with respect to </strong><strong>(x_1)</strong><strong> on the left hand side of </strong><strong>(=)</strong><strong>. The right hand side of </strong><strong>(=)</strong><strong> must be your expression for the partial first derivative.</strong>

<strong>NOTE:</strong> The “partial” operator, (partial) is created by typing partial.

<em>HINT</em>: The partial derivative “fraction” should look like:

[ frac{partial f}{partial x_1} ]

<h4>SOLUTION</h4>

[ HERE ]

<h3>6b)</h3>

Now write out the expression for the partial derivative of (f) with respect to (x_2).

<h4>PROBLEM</h4>

<strong>Write out the partial derivative of </strong><strong>(f)</strong><strong> with respect to </strong><strong>(x_2)</strong><strong>. To receive full credit you must use the </strong><strong>frac{}{}</strong><strong> to write out the partial derivative of </strong><strong>(f)</strong><strong> with respect to </strong><strong>(x_2)</strong><strong> on the left hand side of </strong><strong>(=)</strong><strong>. The right hand side of </strong><strong>(=)</strong><strong> must be your expression for the partial first derivative.</strong>

<strong>NOTE:</strong> The “partial” operator, (partial) is created by typing partial.

<h4>SOLUTION</h4>

[ HERE ]

<h3>6c)</h3>

As discussed in lecture, we also need to work with second derivatives. The expression for the “fraction” for the partial second derivative of (f) with respect to (x_1) is written as:

[ frac{partial^{2} f}{partial x_{1}^{2}} ]

<h4>PROBLEM</h4>

<strong>Write out the partial second derivative of </strong><strong>(f)</strong><strong> with respect to </strong><strong>(x_1)</strong><strong>. Remember that the second derivative is the derivative of the first derivative.</strong>

<h4>SOLUTION</h4>

[ HERE ]

<h3>6d)</h3>

The second derivative in 6c) represents the rate-of-change with respect to (x_1) of the rate-of-change with respect to (x_1). We can also consider the cross-derivative, which examines the rate-of-change with respect to (x_2) of the rate-of-change with respect to (x_1). As a hint, the “fraction” for the cross-derivative looks like:

[ frac{partial^2 f}{partial x_1 partial x_2} ]

<h4>PROBLEM</h4>

<strong>What is the cross derivative equal to, for the example function of two variables? Write out the expression within an equation block below.</strong>

<h4>SOLUTION</h4>

[ HERE ]

<h3>6e)</h3>

In lecture, we also reviewed important linear algebra concepts. We discussed the inner product, and how we can write it out two ways. One approach is with vector-vector math, while the other involves a summation. For the next several problems you will work with a vector (mathbf{x}) which is a (left(N times 1right)) column vector.

<h4>PROBLEM</h4>

<strong>Write out the vector-vector operation for the inner product of the vector </strong><strong>(mathbf{x})</strong><strong> with itself. Place your expression within an equation block below. You do not need to write out the elements of the vectors.</strong>

<h4>SOLUTION</h4>

[ HERE ]

<h3>6f)</h3>

The summation approach to writing the inner product is displayed for you below:

[ HERE ]

The summation expression consists of three components. The first is the Sigma character, which is created by the typing sum. If we want the sigma character to appear in line, we wrap dollar signs around it, $sum$, and if we want it to appear within an equation block we wrap two dollar signs, $$sum$$. The (n=1) and (N) characters are displayed below and above the Sigma character with the _ and ^ special characters, respectively.

<h4>PROBLEM</h4>

<strong>Write out the summation approach to the inner product within an equation block below.</strong>

<h4>SOLUTION</h4>

[ HERE ]

<h3>6g)</h3>

In the 6e), the vector (mathbf{x}) was defined to be a (left(N times 1 right)) column vector. What are the dimensions of the inner product of (mathbf{x}) with itself? What would the dimensions of the outer product of (mathbf{x}) be with itself?

<h4>PROBLEM</h4>

<strong>Write the dimensions of the inner product and the dimensions of the outer product of </strong><strong>(mathbf{x})</strong><strong> with itself. Note that to display the multiplication sign you can type </strong><strong>times</strong><strong>.</strong>

<h4>SOLUTION</h4>

Type your answer here.

<h3>6h)</h3>

We will frequently use greek letters when writing expressions and equations. Thankfully, it is rather simple to type greek letters in LaTeX. All you have to do is type the escape character  in front of the greek word. For example to display (delta), just type $delta$. To show the capital letter (Delta) use a capital D instead of a lower case d: $Delta$.

<h4>PROBLEM</h4>

<strong>Practice typing the greek letters, </strong><strong>(alpha)</strong><strong>, </strong><strong>(beta)</strong><strong>, </strong><strong>(gamma)</strong><strong>, </strong><strong>(epsilon)</strong><strong>, </strong><strong>(mu)</strong><strong>, </strong><strong>(sigma)</strong><strong>, and </strong><strong>(psi)</strong><strong> in an equation block below. Separate each letter by the LaTeX term </strong><strong>cdot</strong><strong> which displays the “dot-multiply” operator, </strong><strong>(cdot)</strong><strong>.</strong>

<em>Hint</em>: the greek words are alpha, beta, gamma, epsilon, mu, sigma, and psi.

<h4>SOLUTION</h4>

[ HERE ]


