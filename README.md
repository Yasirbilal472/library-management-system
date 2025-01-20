import java.util.*;

public class LibraryManagement {
    private static Scanner scanner = new Scanner(System.in);
    private static Map<String, String> librarians = new HashMap<>(); // Stores librarian credentials
    private static Map<String, Map<String, String>> books = new HashMap<>(); // Stores books with ISBN as key and details as value
    private static List<Map<String, String>> members = new ArrayList<>(); // Stores member details
    private static List<Map<String, String>> issuedBooks = new ArrayList<>(); // Stores issued book details

    public static void main(String[] args) {
        // Adding a default librarian for login
        librarians.put("admin", "password");

        if (validateLibrarian()) {
            menu();
        } else {
            System.out.println("Invalid credentials. Please try again.");
        }
    }

    private static boolean validateLibrarian() {
        System.out.println("Enter librarian username:");
        String username = scanner.nextLine();
        System.out.println("Enter librarian password:");
        String password = scanner.nextLine();
        return librarians.containsKey(username) && librarians.get(username).equals(password);
    }

    private static void menu() {
        while (true) {
            System.out.println("\nLibrary Management Menu:");
            System.out.println("1. Add a Book");
            System.out.println("2. Display Books");
            System.out.println("3. Issue a Book");
            System.out.println("4. Return a Book");
            System.out.println("5. Add Librarian");
            System.out.println("6. Remove Librarian");
            System.out.println("7. Add Member");
            System.out.println("8. Display Members");
            System.out.println("9. Display Librarians");
            System.out.println("10. Remove a Book");
            System.out.println("11. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume the newline

            switch (choice) {
                case 1:
                    addBook();
                    break;
                case 2:
                    displayBooks();
                    break;
                case 3:
                    issueBook();
                    break;
                case 4:
                    returnBook();
                    break;
                case 5:
                    addLibrarian();
                    break;
                case 6:
                    removeLibrarian();
                    break;
                case 7:
                    addMember();
                    break;
                case 8:
                    displayMembers();
                    break;
                case 9:
                    displayLibrarians();
                    break;
                case 10:
                    removeBook();
                    break;
                case 11:
                    System.out.println("Exiting... Goodbye!");
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }

    private static void addBook() {
        System.out.println("Enter the ISBN of the book:");
        String isbn = scanner.nextLine();
        System.out.println("Enter the name of the book:");
        String bookName = scanner.nextLine();
        System.out.println("Enter the author of the book:");
        String author = scanner.nextLine();

        Map<String, String> bookDetails = new HashMap<>();
        bookDetails.put("name", bookName);
        bookDetails.put("author", author);

        books.put(isbn, bookDetails);
        System.out.println("Book added successfully.");
    }

    private static void displayBooks() {
        if (books.isEmpty()) {
            System.out.println("No books available in the library.");
        } else {
            System.out.println("Books in the library:");
            for (Map.Entry<String, Map<String, String>> entry : books.entrySet()) {
                String isbn = entry.getKey();
                Map<String, String> details = entry.getValue();
                System.out.println("ISBN: " + isbn + ", Name: " + details.get("name") + ", Author: " + details.get("author"));
            }
        }
    }

    private static void issueBook() {
        System.out.println("Enter the ISBN of the book to issue:");
        String isbn = scanner.nextLine();
        if (books.containsKey(isbn)) {
            System.out.println("Enter the member name:");
            String memberName = scanner.nextLine();
            System.out.println("Enter the member ID:");
            String memberId = scanner.nextLine();
            System.out.println("Enter the issue date (YYYY-MM-DD):");
            String issueDate = scanner.nextLine();
            System.out.println("Enter the expected return date (YYYY-MM-DD):");
            String returnDate = scanner.nextLine();

            Map<String, String> issuedBook = new HashMap<>();
            issuedBook.put("isbn", isbn);
            issuedBook.put("memberName", memberName);
            issuedBook.put("memberId", memberId);
            issuedBook.put("issueDate", issueDate);
            issuedBook.put("returnDate", returnDate);

            issuedBooks.add(issuedBook);
            books.remove(isbn);
            System.out.println("Book issued successfully.");
        } else {
            System.out.println("Book not available.");
        }
    }

    private static void returnBook() {
        System.out.println("Enter the ISBN of the book to return:");
        String isbn = scanner.nextLine();
        System.out.println("Enter the name of the book:");
        String bookName = scanner.nextLine();
        System.out.println("Enter the author of the book:");
        String author = scanner.nextLine();

        Map<String, String> bookDetails = new HashMap<>();
        bookDetails.put("name", bookName);
        bookDetails.put("author", author);

        books.put(isbn, bookDetails);
        System.out.println("Book returned successfully.");
    }

    private static void addLibrarian() {
        System.out.println("Enter new librarian username:");
        String username = scanner.nextLine();
        System.out.println("Enter new librarian password:");
        String password = scanner.nextLine();
        librarians.put(username, password);
        System.out.println("Librarian added successfully.");
    }

    private static void removeLibrarian() {
        System.out.println("Enter the username of the librarian to remove:");
        String username = scanner.nextLine();
        if (librarians.containsKey(username)) {
            librarians.remove(username);
            System.out.println("Librarian removed successfully.");
        } else {
            System.out.println("Librarian not found.");
        }
    }

    private static void addMember() {
        System.out.println("Enter the name of the member:");
        String memberName = scanner.nextLine();
        System.out.println("Enter the contact number of the member:");
        String contactNumber = scanner.nextLine();
        System.out.println("Enter the ID number of the member:");
        String memberId = scanner.nextLine();

        Map<String, String> memberDetails = new HashMap<>();
        memberDetails.put("name", memberName);
        memberDetails.put("contact", contactNumber);
        memberDetails.put("id", memberId);

        members.add(memberDetails);
        System.out.println("Member added successfully.");
    }

    private static void displayMembers() {
        if (members.isEmpty()) {
            System.out.println("No members available.");
        } else {
            System.out.println("Library Members:");
            for (Map<String, String> member : members) {
                System.out.println("Name: " + member.get("name") + ", Contact: " + member.get("contact") + ", ID: " + member.get("id"));
            }
        }
    }

    private static void displayLibrarians() {
        System.out.println("List of Librarians:");
        for (String username : librarians.keySet()) {
            System.out.println(username);
        }
    }

    private static void removeBook() {
        System.out.println("Enter the ISBN of the book to remove:");
        String isbn = scanner.nextLine();
        if (books.remove(isbn) != null) {
            System.out.println("Book removed successfully.");
        } else {
            System.out.println("Book not found.");
        }
    }
}
