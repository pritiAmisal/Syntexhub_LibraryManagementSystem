package library;

import java.util.ArrayList;
import java.util.Scanner;

//BOOK CLASS 
class Book {
    private String title;
    private String author;
    private boolean isAvailable;

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
        this.isAvailable = true;
    }

    public String getTitle() {
        return title;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void setAvailable(boolean status) {
        isAvailable = status;
    }

    @Override
    public String toString() {
        return "Title: " + title +
               ", Author: " + author +
               ", Available: " + (isAvailable ? "Yes" : "No");
    }
}

//LIBRARY CLASS 
class Library {
    private ArrayList<Book> books = new ArrayList<>();

    public void addBook(String title, String author) {
        books.add(new Book(title, author));
        System.out.println("Book added successfully");
    }

    public void displayBook() {
        if (books.isEmpty()) {
            System.out.println("No books available in the library");
            return;
        }
        for (Book book : books) {
            System.out.println(book);
        }
    }

    public void borrowBook(String title) {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title)) {
                if (book.isAvailable()) {
                    book.setAvailable(false);
                    System.out.println("Book borrowed successfully");
                } else {
                    System.out.println("Book already borrowed");
                }
                return;
            }
        }
        System.out.println("Book not found");
    }

    public void returnBook(String title) {
        for (Book book : books) {
            if (book.getTitle().equalsIgnoreCase(title)) {
                if (!book.isAvailable()) {
                    book.setAvailable(true);
                    System.out.println("Book returned successfully");
                } else {
                    System.out.println("Book was not borrowed");
                }
                return;
            }
        }
        System.out.println("Book not found");
    }
}

//MAIN CLASS
public class LibraryManagementSystem {

    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {

        Library library = new Library();
        boolean exit = false;

        while (!exit) {
            System.out.println("\n==== Library Management System ====");
            System.out.println("1. Add Book");
            System.out.println("2. Display Books");
            System.out.println("3. Borrow Book");
            System.out.println("4. Return Book");
            System.out.println("5. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // clear buffer

            switch (choice) {
                case 1:
                    addBookToLibrary(library);
                    break;
                case 2:
                    library.displayBook();
                    break;
                case 3:
                    borrowBookFromLibrary(library);
                    break;
                case 4:
                    returnBookToLibrary(library);
                    break;
                case 5:
                    exit = true;
                    System.out.println("Exiting Library Management System");
                    break;
                default:
                    System.out.println("Invalid choice");
            }
        }
        scanner.close();
    }

    //HELPER METHODS
    private static void addBookToLibrary(Library library) {
        System.out.print("Enter book title: ");
        String title = scanner.nextLine();
        System.out.print("Enter author name: ");
        String author = scanner.nextLine();
        library.addBook(title, author);
    }

    private static void borrowBookFromLibrary(Library library) {
        System.out.print("Enter book title to borrow: ");
        String title = scanner.nextLine();
        library.borrowBook(title);
    }

    private static void returnBookToLibrary(Library library) {
        System.out.print("Enter book title to return: ");
        String title = scanner.nextLine();
        library.returnBook(title);
    }
}