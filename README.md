# LearnerAcademy
Login Page

package userManagement.servlet;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class LogIn_Page
 */
@WebServlet("/LogIn_Page")
public class LogIn_Page extends HttpServlet {
	private static final long serialVersionUID = 1L;

	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String email = request.getParameter("email");
		String password = request.getParameter("password");

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();
		if (email.equals("example@gmail.com") && password.equals("123")) {
			RequestDispatcher rd = request.getRequestDispatcher("Home_Page.jsp");
			rd.forward(request, response);

		} else {
			out.print("<p style='color:red;'>Invalid Email & Password</p>");
			RequestDispatcher rd = request.getRequestDispatcher("SignIn-Page.jsp");
			rd.include(request, response);
		}out.close();
	}
}


========================================================================
Connection Provider

package servlet.jdbc.ConnectionClass;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;


public class ConnectionProvider {
	public static Connection conn;

	public static Connection CreateConnection() throws SQLException {
		final String JDBC_LoadDriver = "com.mysql.cj.jdbc.Driver";
		final String Connection_URL = "jdbc:mysql://localhost:3306/student_db";
		final String MYSQL_User = "root";
		final String MYSQL_Password = "root";
		try {
			// driver load
			Class.forName(JDBC_LoadDriver);
			// connection creating
			conn = DriverManager.getConnection(Connection_URL, MYSQL_User, MYSQL_Password);
		} catch (ClassNotFoundException e) {
			System.out.println(e);
			e.printStackTrace();
		}
		return conn;
	}

}

========================================================================
Delete Student

package servlet.jdbc.input;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import servlet.jdbc.StudentDAO.StudentDAO;

/**
 * Servlet implementation class DeleteStudent
 */
@WebServlet("/DeleteStudent")
public class DeleteStudent extends HttpServlet {
	private static final long serialVersionUID = 1L;

	/**
	 * @see HttpServlet#HttpServlet()
	 */
	public DeleteStudent() {
		super();
		// TODO Auto-generated constructor stub
	}

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		int id = Integer.parseInt(request.getParameter("id"));
		boolean ans = StudentDAO.DeleteStudentFromDB(id);

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		if (ans == true) {
			out.print("<h3>Successfully Deleted</h3>");
			RequestDispatcher rd = request.getRequestDispatcher("Delete_Data.jsp");
			rd.include(request, response);
		} else {
			out.print("<h3>Not Deleted</h3>");
			RequestDispatcher rd = request.getRequestDispatcher("Delete_Data.jsp");
			rd.include(request, response);
		}

	}
}

========================================================================
Student Registration

package servlet.jdbc.input;

import java.io.IOException;
import java.io.PrintWriter;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import servlet.jdbc.StudentDAO.StudentDAO;
import servlet.jdbc.student.StudentEntity;

/**
 * Servlet implementation class StudentRegisteration
 */
@WebServlet("/StudentRegisteration")
public class StudentRegisteration extends HttpServlet {
	private static final long serialVersionUID = 1L;

	/**
	 * @see HttpServlet#HttpServlet()
	 */
	public StudentRegisteration() {
		super();
		// TODO Auto-generated constructor stub
	}

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		String name = request.getParameter("name");
		String contact = request.getParameter("contact");
		String email = request.getParameter("email");
		String course = request.getParameter("course");
		String batch = request.getParameter("batch");

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		StudentEntity st = new StudentEntity(name, contact, email, course, batch);
		System.out.println(st);
		boolean ans = StudentDAO.InsertStudentIntoDB(st);

		if (ans == true) {
			out.print("<h3>Successfully Inserted</h3>");
			RequestDispatcher rd = request.getRequestDispatcher("Add_Data.jsp");
			rd.include(request, response);
		} else {
			out.print("<h3>Failed Inserted</h3>");
			RequestDispatcher rd = request.getRequestDispatcher("Add_Data.jsp");
			rd.include(request, response);
		}
	}
}

========================================================================
Student update

package servlet.jdbc.input;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import servlet.jdbc.StudentDAO.StudentDAO;
import servlet.jdbc.student.StudentEntity;

/**
 * Servlet implementation class UpdateStudent
 */
@WebServlet("/UpdateStudent")
public class UpdateStudent extends HttpServlet {
	private static final long serialVersionUID = 1L;

	/**
	 * @see HttpServlet#HttpServlet()
	 */
	public UpdateStudent() {
		super();
		// TODO Auto-generated constructor stub
	}

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		// TODO Auto-generated method stub
		response.getWriter().append("Served at: ").append(request.getContextPath());
	}

	/**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		int id = Integer.parseInt(request.getParameter("id"));
		String name = request.getParameter("name");
		String contact = request.getParameter("contact");
		String email = request.getParameter("email");
		String course = request.getParameter("course");
		String batch = request.getParameter("batch");

		response.setContentType("text/html");
		PrintWriter out = response.getWriter();

		StudentEntity st = new StudentEntity(id, name, contact, email, course, batch);
		System.out.println(st);
		boolean ans = StudentDAO.UpdateStudentIntoDB(st);
		if (ans == true) {
			out.print("<h3>Successfully Updated</h3>");
			RequestDispatcher rd = request.getRequestDispatcher("Show_Data.jsp");
			rd.include(request, response);
		} else {
			out.print("<h3>Failed Updation</h3>");
			RequestDispatcher rd = request.getRequestDispatcher("Edit_Data.jsp");
			rd.include(request, response);
		}
	}
}

========================================================================
Student Entity

package servlet.jdbc.student;
public class StudentEntity {
	private int id;
	private String name, contact, email, course, batch;
	public StudentEntity() {
		super();
	}
	public StudentEntity(String name, String contact, String email, String course, String batch) {
		super();
		this.name = name;
		this.contact = contact;
		this.email = email;
		this.course = course;
		this.batch = batch;
	}
	public StudentEntity(int id, String name, String contact, String email, String course, String batch) {
		super();
		this.id = id;
		this.name = name;
		this.contact = contact;
		this.email = email;
		this.course = course;
		this.batch = batch;
	}
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getContact() {
		return contact;
	}
	public void setContact(String contact) {
		this.contact = contact;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getCourse() {
		return course;
	}
	public void setCourse(String course) {
		this.course = course;
	}
	public String getBatch() {
		return batch;
	}
	public void setBatch(String batch) {
		this.batch = batch;
	}
	@Override
	public String toString() {
		return "StudentEntity [id=" + id + ", name=" + name + ", contact=" + contact + ", email=" + email + ", course="
				+ course + ", batch=" + batch + "]";
	}
}
========================================================================
DAO

package servlet.jdbc.StudentDAO;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.mysql.cj.protocol.Resultset;

import servlet.jdbc.ConnectionClass.ConnectionProvider;
import servlet.jdbc.student.StudentEntity;

public class StudentDAO {
	public static boolean InsertStudentIntoDB(StudentEntity student) {
		boolean ans = false;
		try {
			Connection conn = ConnectionProvider.CreateConnection();
			String InsertData = "insert into student_detail (name, contact, email, course, batch) values(?,?,?,?,?);";
			PreparedStatement stmt = conn.prepareStatement(InsertData);

			stmt.setString(1, student.getName());
			stmt.setString(2, student.getContact());
			stmt.setString(3, student.getEmail());
			stmt.setString(4, student.getCourse());
			stmt.setString(5, student.getBatch());
			stmt.executeUpdate();
			return ans = true;

		} catch (SQLException e) {
			e.printStackTrace();
		}
		return ans;
	}

	public static boolean DeleteStudentFromDB(int id) {
		boolean ans = false;
		try {
			Connection conn = ConnectionProvider.CreateConnection();
			String DeleteData = "delete from student_detail where id=?";
			PreparedStatement stmt = conn.prepareStatement(DeleteData);
			stmt.setInt(1, id);
			stmt.executeUpdate();
			ans = true;
		} catch (Exception e) {
			System.out.println(e);
			e.printStackTrace();
		}
		return ans;
	}

	public static Boolean ShowData() {
		boolean ans = false;
		try {
			Connection conn = ConnectionProvider.CreateConnection();
			String ShowData = "select * from student_detail";
			Statement stmt = conn.createStatement();
			ResultSet rs = stmt.executeQuery(ShowData);
			while (rs.next()) {
				int id = rs.getInt(1);
				String name = rs.getString(2);
				String contact = rs.getString(3);
				String email = rs.getString(4);
				String course = rs.getString(5);
				String batch = rs.getString(6);
				System.out.println(id + " " + name + " " + contact + " " + email + " " + course + " " + batch);
			}

		} catch (SQLException e) {
			e.printStackTrace();
		}
		return null;
	}

	public static boolean UpdateStudentIntoDB(StudentEntity student) {
		boolean ans = false;
		try {
			Connection conn = ConnectionProvider.CreateConnection();
			String updatedata = "update student_detail set name=?, contact=?, email=?, course=?, batch=? where id=?";
			PreparedStatement stmt = conn.prepareStatement(updatedata);

			stmt.setString(1, student.getName());
			stmt.setString(2, student.getContact());
			stmt.setString(3, student.getEmail());
			stmt.setString(4, student.getCourse());
			stmt.setString(5, student.getBatch());
			stmt.setInt(6, student.getId());

			stmt.executeUpdate();
			return ans = true;

		} catch (SQLException e) {
			e.printStackTrace();
		}
		return ans;
	}
}

========================================================================


All JSP Pages

Add_Data.jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Adding Data</title>
</head>
<style>
body {
	border-style:double; padding: 5mm;border-radius:5mm;
}
</style>
<body>
<%@ include file="Main-Header.jsp" %>
<%@ include file="Menu.jsp" %>
<form action="StudentRegisteration" method="post">
<p style="color: orange;">Fill Student Detail</p>
<hr style="color: purple;">
<img alt="add image" src="iStock-1150384596-2.jpg" height="300" width="450" align="right">
<b>Student Name</b><br>
<input type="text" name="name" size="30"><br>
<b>Student Contact Number</b><br>
<input type="text" name="contact" size="30"><br>
<b>Student Email</b><br>
<input type="email" name="email" size="30"><br>
<b>Select Course</b><br>
<select name="course">
<option >----</option>
<option>Java</option>
<option>Python</option>
<option>Php</option>
<option>JavaScript</option>
</select><br>
<b>Select Batch Type</b><br>
<select name="batch">
<option>Regular</option>
<option>WeekEnd</option>
</select><br><br>
<input type="submit" value="Register">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<input type="reset" value="Clear All">
</form>
</body>
</html>
========================================================================
Delete_Data.jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Delete Data</title>
</head>
<style>
body {
	border-style:double; padding: 5mm;border-radius:5mm;
}
</style>
<body>
<%@ include file="Main-Header.jsp" %>
<%@ include file="Menu.jsp" %>
<form action="DeleteStudent" method="post">
<h1>Delete data</h1>
Enter ID <input type="text" name="id">
<input type="submit" value="ok">
</form>
</body>
</html>
========================================================================
Home_Page.jsp

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Home Page</title>
</head>
<%@ include file="Main-Header.jsp" %>
<style>
body {
	border-style:double; padding: 5mm;border-radius:5mm;
}
</style>
<body>
<%@ include file="Menu.jsp" %>
<form action="action">
<h1>Welcome To Learner's Academy Admin Portal</h1>
<p style="color: green;">Developed By : Shatrudhan Verma</p>
<p>Email : skv@gmail.com</p>
</form>
</body>
</html>
========================================================================
Main_Header.jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<h1 style="border-style: solid;padding: 5mm;border-radius: 5mm;background-color:blue;color: white;">Learner's Academy</h1>
<p style="border-style:solid; padding: 2mm;background-color:teal;color :white; ;border-radius: 3mm" align="right">Developed By: Shatrudhan Verma &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Email : skv@gmail.com</p>
</body>
</html>
========================================================================
Menu.jsp

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Menu Bar</title>
</head>
<body >
<form action="action">
<h3 style="border-style: solid;border-radius: 5mm; padding: 5mm;">
<a href="Home_Page.jsp" style="padding: 5mm;">Home</a>
<a href="Add_Data.jsp" style="padding: 5mm;">Add Data</a>
<a href="Show_Data.jsp" style="padding: 5mm;">Show Data</a>
<!-- <a href="UpdateStudent.jsp" style="padding: 5mm;">Update Data</a> -->
<a href="Delete_Data.jsp" style="padding: 5mm;">Delete Data</a>
<a href="SignIn-Page.jsp" style="padding: 5mm;color: red;">LogOut</a>
<h3>
</form>
</body>
</html>
========================================================================
Show_Data.jsp

<%@page import="java.sql.Statement"%>
<%@page import="java.sql.*"%>
<%@page import="java.sql.PreparedStatement"%>
<%@page import="servlet.jdbc.ConnectionClass.ConnectionProvider"%>
<%-- <%@page import="servlet.jdbc.input.ShowStudentData"%>--%>
<%@page import="servlet.jdbc.StudentDAO.StudentDAO"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Data Display</title>
</head>
<style>
body {
	border-style:double; padding: 5mm;border-radius:5mm;
}
</style>
<body>
<%@ include file="Main-Header.jsp" %>
<%@ include file="Menu.jsp" %>
<form action="ShowStudentData" method="post">
<h1>show data</h1>
<p>Double tap on show data to refresh page</p>
<table style="color: blue; border-color: blue;" border="1">
<tr style="color: white; background-color:blue; ">
	 <th>Student ID</th>
	 <th>Name</th>
	 <th>Contact</th>
	 <th>Email</th>
	 <th>Course</th>
	 <th>Batch Timing</th>
	 <th>Update Data</th>
</tr>
<%
try{
	String ShowData = "select * from student_detail";
	Connection conn=ConnectionProvider.CreateConnection();
	Statement stmt= conn.createStatement();
	ResultSet rs=stmt.executeQuery(ShowData);
	
	while(rs.next()){
		%> <tr style="color: black;">
<td><%= rs.getInt(1)%></td>
<td><%= rs.getString(2)%></td>
<td><%= rs.getString(3)%></td>
<td><%= rs.getString(4)%></td>
<td><%= rs.getString(5)%></td>
<td><%= rs.getString(6)%></td>
<td><a href="UpdateStudent.jsp">Edit</a></td>
</tr>
<%
	}
}catch(Exception e){
	out.print(e);
}
%>
</table>
</form>
</body>
</html>
========================================================================
SignIn-Page.jsp

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>LogIn Page</title>
</head>
<style>
body {
	border-style:double; padding: 5mm;border-radius:5mm;
}
</style>
<body>
<%@ include file="Main-Header.jsp" %>
<form action="LogIn_Page" method="post">
<hr>
<b>User Email</b><br>
<input type="email" name="email" placeholder="example@email.com" size="30"><br><br>
<b>User Password</b><br>
<input type="password" name="password" placeholder="123" size="30"><br><br>
<input type="submit" value="LogIn">
</form>
</body>
</html>
========================================================================
UpdateStudent.jsp

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<style>
body {
	border-style:double; padding: 5mm;border-radius:5mm;
}
</style>
<body>
<%@ include file="Main-Header.jsp" %>
<%@ include file="Menu.jsp" %>
<form action="UpdateStudent" method="post">
<p style="color: orange;">Fill Student Detail to update record</p>
<hr style="color: purple;">
<img alt="add image" src="student-working-laptop-white-background.webp" height="300" width="450" align="right">
<p style="color: red;">Note : Student ID must be same from which you want replace Data</p>
<b>Student Existing ID</b><br>
<input type="text" name="id" size="30"><br>
<b>Student Name</b><br>
<input type="text" name="name" size="30"><br>
<b>Student Contact Number</b><br>
<input type="text" name="contact" size="30"><br>
<b>Student Email</b><br>
<input type="email" name="email" size="30"><br>
<b>Select Course</b><br>
<select name="course">
<option >----</option>
<option>Java</option>
<option>Python</option>
<option>Php</option>
<option>JavaScript</option>
</select><br>
<b>Select Batch Type</b><br>
<select name="batch">
<option>Regular</option>
<option>WeekEnd</option>
</select><br><br>
<input type="submit" value="Update">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
<input type="reset" value="Clear All">
</form>
</body>
</html>
========================================================================

Pom.xml

<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
<modelVersion>4.0.0</modelVersion>
<groupId>User-Management</groupId>
<artifactId>User-Management</artifactId>
<version>0.0.1-SNAPSHOT</version>
<packaging>war</packaging>
<name>User-Management</name>
<description>User-Management</description>
<dependencies>
	 <!-- https://mvnrepository.com/artifact/javax.servlet/javax.servlet-api -->
<dependency>
<groupId>javax.servlet</groupId>
<artifactId>javax.servlet-api</artifactId>
<version>4.0.1</version>
<scope>provided</scope>
</dependency>
<!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
<dependency>
<groupId>com.mysql</groupId>
<artifactId>mysql-connector-j</artifactId>
<version>8.0.32</version>
</dependency>
	
</dependencies>
<build>
<plugins>
<plugin>
<artifactId>maven-compiler-plugin</artifactId>
<version>3.8.1</version>
<configuration>
<release>17</release>
</configuration>
</plugin>
<plugin>
<artifactId>maven-war-plugin</artifactId>
<version>3.2.3</version>
</plugin>
</plugins>
</build>
</project>
================================
