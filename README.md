HERE'S HOW IT LOOKS
https://github.com/user-attachments/assets/b649a8d5-d7ec-4c89-a636-9a6115421fb7
package com.scb.Payment.Initiation.Entity;

import jakarta.persistence.*;
import java.util.Set;

@Entity
@Table(name = "users")  // assuming your table name is "users"
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long userId;

    private String username;

    private String email;

    // other fields like password, etc.

    // One user can have many userRoles
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL, orphanRemoval = true)
    private Set<UserRole> userRoles;

    // Constructors, getters, setters

    public User() {}

    // getters and setters
    public Long getUserId() {
        return userId;
    }
    public void setUserId(Long userId) {
        this.userId = userId;
    }

    public String getUsername() {
        return username;
    }
    public void setUsername(String username) {
        this.username = username;
    }

    public String getEmail() {
        return email;
    }
    public void setEmail(String email) {
        this.email = email;
    }

    public Set<UserRole> getUserRoles() {
        return userRoles;
    }
    public void setUserRoles(Set<UserRole> userRoles) {
        this.userRoles = userRoles;
    }
}

