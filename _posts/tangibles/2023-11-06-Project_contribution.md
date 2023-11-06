---
toc: true
comments: false
layout: post
title: Passion project contribution
description: Notes and reflections from the passion project code that I developed.
type: tangibles
courses: { compsci: {week: 12} }
---

# Fiction menu:

```
<style>/*styling for button*/
    .button {
  background-color: #4CAF50; /* Green */
  border: none;
  color: rgb(57, 244, 10);
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  -webkit-transition-duration: 0.4s; /* Safari */
  transition-duration: 0.4s;
  
}
.button2:hover {/*creates a shadow when hovering over it*/
    box-shadow: 0 12px 16px 0 rgba(255, 255, 255, 0.19),0 17px 50px 0 rgba(255, 255, 255, 0.19);
  }
</style>

<!--136, 255, 0, 0.19 - For green-->

<table>
    <tr> <!--The 'class' gives the styling info to the buttons-->
        <td><a href="{{site.baseurl}}/basics/home">Home</a></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/action">Action and adventure</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/contemporary">Contemporary fiction</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/dystopian">Dystopian</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/fantasy">Fantasy</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/graphicnovel">Graphic novel</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/historical">Historical fiction</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/horror">Horror</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/magicalrealism">Magical realism</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/mystery">Mystery</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/newadult">New adult</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/romance">Romance</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/scifi">Science fiction</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/thriller">Thriller and suspense</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/women">Women's fiction</a></button></td>
        <td><button class="button button2"><a href="{{site.baseurl}}/basics/youngadult">Young adult</a></button></td>
    </tr>
</table>

<script>
  // Function to alphabetically order the sub-categories
  function orderSubCategories() {
      var table = document.querySelector("table");
      var rows = Array.from(table.rows);
      rows.shift(); // Remove the header row

      rows.sort(function(a, b) {
          var textA = a.textContent.toLowerCase();
          var textB = b.textContent.toLowerCase();
          return textA.localeCompare(textB);
      });

      // Clear the current table
      while (table.firstChild) {
          table.removeChild(table.firstChild);
      }

      // Add rows back to the table in sorted order
      rows.forEach(function(row) {
          table.appendChild(row);
      });
  }

  orderSubCategories();
</script>
```

This code created the menu for the fiction books. As seen in the code, each genre of fiction has its own button pertaining to a permalink, which allows for the `.md` file of each genre to be accessed when the appropriate button in this menu is clicked. I improved my code by integrated CSS styling using some help from ChatGPT to make the UI look more welcoming and professional. Furthermore, the JavaScript code at the end of the program sorts all the buttons by alphabetical order.

<strong>Errors</strong>: No major errors other than mismatching permalinks, resulting in some of the buttons leading to the wrong `.md` file.


# Fiction .md file and developed the Home Page:

<blockquote class="imgur-embed-pub" lang="en" data-id="1c52Rxo"><a href="https://imgur.com/1c52Rxo">View post on imgur.com</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>
These were all the files that I created for each genre in fiction.

# Example of code for each genre:

```
{% include nav_basics.html %}

<html>
<head>
    <!-- load jQuery and DataTables output style and scripts -->
    <!-- The line below styles the table -->
    <link rel="stylesheet" type="text/css" href="https://cdn.datatables.net/1.13.4/css/jquery.dataTables.min.css">
    <!-- Brings out a tool from jQuery to help change the way the table looks -->
    <script type="text/javascript" language="javascript" src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script>var define = null;</script>
    <script type="text/javascript" language="javascript" src="https://cdn.datatables.net/1.13.4/js/jquery.dataTables.min.js"></script>
</head>
<body>
    <table id="demo" class="table">
        <thead>
            <tr>
                <th>Book Author</th>
                <th>Book Title</th>
                <th>Cover</th>
                <th>Blurb</th>
            </tr>
        </thead>
        <tbody id="tabledata">

        </tbody>
    </table>

    <script>
        var api = 'https://bookbattles.stu.nighthawkcodingsociety.com/api/books/';
        var tableBody = document.getElementById("tabledata");

        function fillTable() {
            fetch(api)
                .then(response => response.json())
                .then(data => {
                    data.forEach(function(book) {
                        if (book.genres.includes("dystopian")) {
                            var table_row = document.createElement("tr");
                            var author = document.createElement("td");
                            var title = document.createElement("td");
                            var coverCell = document.createElement("td");
                            var blurb = document.createElement("td");

                            author.innerHTML = book.book_author;
                            title.innerHTML = book.book_title;
                            coverCell.innerHTML = '<img src="' + book.cover_url + '" alt="Book Cover" style="width:50px;height:50px;">';
                            blurb.innerHTML = book.blurb;

                            table_row.appendChild(author);
                            table_row.appendChild(title);
                            table_row.appendChild(coverCell);
                            table_row.appendChild(blurb);

                            tableBody.appendChild(table_row);
                        }
                    });

                    $('#demo').DataTable();
                })
                .catch(error => console.error('Error fetching data:', error));
        }

        fillTable();
    </script>
</body>
</html>
```

This is the code for the dystopian fiction genre (it is the same for all other genres - the only thing that changed for each genre was line 135: `if (book.genres.includes("dystopian")) {`). In this program, I began with the CSS styling for the table and create the "Book Author", "Book Title", "Cover" and "Blurb" columns. I called the API with the `fetch()` command and filled in each column with the appropriate information using JavaScript.

<strong>Errors</strong>: I forgot to include "% include nav_basics.html %" at the top of the code, which resulted in nothing showing up for each genre. By including that line of code, the permalink was called back in `nav_fiction.html` and all the information was displayed.

# Button styling:

```
<html>
<head>
    <style>
        /* Style the link as a fancy button */
        .fancy-button-link {
            display: inline-block;
            padding: 12px 24px;
            background-color: #007BFF;
            color: #fff;
            text-decoration: none;
            border: 2px solid #FF00FF;
            border-radius: 50px; /* Rounded shape */
            text-align: center;
            font-size: 18px;
            font-weight: bold;
            letter-spacing: 1px;
            transition: background-color 0.3s, color 0.3s, transform 0.3s;
        }

        /* Change the button style on hover */
        .fancy-button-link:hover {
            background-color: #0056b3;
            color: #fff;
            transform: scale(1.05); /* Scale up the button on hover */
        }
    </style>
</head>
<body>
    <a class="button-link" href="http://127.0.0.1:4100/frontend_shared//basics/home">BookBattles Lobby - Start your journey here!</a>
</body>
</html> <br>

    
<html>
<head>
    <style>
        /* Style the link as a button */
        .button-link {
            display: inline-block;
            padding: 10px 20px; /* Adjust the padding to your liking */
            background-color: #FF00FF; /* Button background color */
            color: #fff; /* Button text color */
            text-decoration: none;
            border: none;
            border-radius: 5px; /* Rounded corners */
            cursor: pointer;
            text-align: center;
            font-size: 16px;
        }

        /* Change the button style on hover */
        .button-link:hover {
            background-color: #0056b3; /* Button background color on hover */
        }
    </style>
</head>
<body>
    <a class="button-link" href="http://127.0.0.1:4100/frontend_shared//2023/10/16/Book_Genres_IPYNB_2_.html">Explore Book Genres</a>
</body>
</html><br>

<html>
<head>
    <style>
        /* Style the link as a button */
        .button-link {
            display: inline-block;
            padding: 10px 20px; /* Adjust the padding to your liking */
            background-color: #FF00FF; /* Button background color */
            color: #fff; /* Button text color */
            text-decoration: none;
            border: none;
            border-radius: 5px; /* Rounded corners */
            cursor: pointer;
            text-align: center;
            font-size: 16px;
        }

        /* Change the button style on hover */
        .button-link:hover {
            background-color: #0056b3; /* Button background color on hover */
        }
    </style>
</head>
<body>
    <a class="button-link" href="http://127.0.0.1:4100/frontend_shared/basics/nextread">Finding Your Next Read</a>
</body><br><br><br><br>

<body>
    <a class="button-link" href="http://127.0.0.1:4100/frontend_shared/basics/blinddate">Blind Book Date</a>
</body>

</html>
```

This code created the styled buttons on the home page for our passion project. I looked for professional-looking CSS styling online and added it to my code.

<strong>Errors</strong>: The formatting for the "button-link" tag went wrong multiple times, which I had to fix.


