import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.PrintWriter;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.swing.JOptionPane;
import javax.swing.JTable;
import javax.swing.table.DefaultTableModel;

public final class two extends javax.swing.JFrame {
    private static javax.swing.JTable usertable; // Define listofusertable as a class-level variable
    
    // Declare a variable to convert the table containing the accounts for approval into DefaultTableModel
    DefaultTableModel listofusertableDTM;

    public two() {
        initComponents(); // Call initComponents from the constructor
        loadCSVData(); // Load CSV data when the class is instantiated
        
        // Initialize the variable holding the default table model
        listofusertableDTM = (DefaultTableModel) listofusertable.getModel();
        
        // Display accounts for approval upon opening the frame
        displayAccountsForApproval();
    }

    // Move this method outside the constructor
    public JTable getListOfUserTable() {
        return listofusertable;
    }

    // Method to add user information to the listofusertable
    public void addUserToTable(String name, String accountNumber, String initial, String pin, String gender, String cardType) {
        DefaultTableModel model = (DefaultTableModel) listofusertable.getModel();
        model.addRow(new Object[]{name, accountNumber, initial, pin, gender, cardType});
    }
    
    public void displayAccountsForApproval() {
        
        // reset the table's contents initially
        listofusertableDTM.setRowCount(0);
        
        // Open a reader to read the accounts for approval
        try {
            BufferedReader reader = new BufferedReader(new FileReader("user.csv"));
            String line;
            
            // Loop through each line
            while ((line = reader.readLine()) != null) {
                String[] accountDetails = line.split(",");
                
                // ONLY DISPLAYS THE ACCOUNTS FOR APPROVAL
                if(accountDetails[7].equals("FOR APPROVAL")) {
                    listofusertableDTM.insertRow(0x0, new Object[] {
                    accountDetails[0],
                    accountDetails[5],
                    accountDetails[3],
                    accountDetails[6],
                    accountDetails[7]
                    });
                }
                
            }
        } catch (IOException ex) {
            Logger.getLogger(two.class.getName()).log(Level.SEVERE, null, ex);
        }
    }

    // Initialize and load data into the table
    private void loadCSVData() {
        DefaultTableModel model = (DefaultTableModel) listofusertable.getModel();
        loadUserInfo("user.csv", model);
    }

    // Load user information from a CSV file into the table
    private void loadUserInfo(String filePath, DefaultTableModel model) {
        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] userInfo = line.split(",");
                if (userInfo.length == 5) {
                    model.addRow(new Object[]{
                        userInfo[0], // Name
                        userInfo[1], // Account Number
                        userInfo[2], // Initial Deposit
                        userInfo[3], // Card Type
                        userInfo[4]  // Account Status                        
                    });
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }


    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jInternalFrame1 = new javax.swing.JInternalFrame();
        jtabbedpane1 = new javax.swing.JTabbedPane();
        two_panel = new javax.swing.JPanel();
        jScrollPane1 = new javax.swing.JScrollPane();
        listofusertable = new javax.swing.JTable();
        approved_bttn2 = new javax.swing.JButton();
        decline_bttn = new javax.swing.JButton();
        jPanel5 = new javax.swing.JPanel();
        back_bttn = new javax.swing.JButton();
        jLabel1 = new javax.swing.JLabel();
        jMenuBar1 = new javax.swing.JMenuBar();
        jMenu1 = new javax.swing.JMenu();
        jMenu2 = new javax.swing.JMenu();

        jInternalFrame1.setVisible(true);

        javax.swing.GroupLayout jInternalFrame1Layout = new javax.swing.GroupLayout(jInternalFrame1.getContentPane());
        jInternalFrame1.getContentPane().setLayout(jInternalFrame1Layout);
        jInternalFrame1Layout.setHorizontalGroup(
            jInternalFrame1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 0, Short.MAX_VALUE)
        );
        jInternalFrame1Layout.setVerticalGroup(
            jInternalFrame1Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 0, Short.MAX_VALUE)
        );

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        getContentPane().setLayout(new org.netbeans.lib.awtextra.AbsoluteLayout());

        jtabbedpane1.setForeground(new java.awt.Color(0, 51, 153));
        jtabbedpane1.setFont(new java.awt.Font("Cinzel Black", 1, 12)); // NOI18N

        two_panel.setForeground(new java.awt.Color(0, 0, 153));
        two_panel.setLayout(new org.netbeans.lib.awtextra.AbsoluteLayout());

        listofusertable.setFont(new java.awt.Font("BankGothic Lt BT", 1, 14)); // NOI18N
        listofusertable.setForeground(new java.awt.Color(0, 33, 62));
        listofusertable.setModel(new javax.swing.table.DefaultTableModel(
            new Object [][] {

            },
            new String [] {
                "ACCOUNT NAME", "ACCOUNT NUMBER", "INITIAL DEPOSIT", "CARD TYPE", "ACCOUNT STATUS"
            }
        ));
        listofusertable.setShowGrid(true);
        jScrollPane1.setViewportView(listofusertable);

        two_panel.add(jScrollPane1, new org.netbeans.lib.awtextra.AbsoluteConstraints(30, 20, 840, 280));

        approved_bttn2.setBackground(new java.awt.Color(0, 51, 153));
        approved_bttn2.setFont(new java.awt.Font("BankGothic Lt BT", 1, 14)); // NOI18N
        approved_bttn2.setForeground(new java.awt.Color(255, 255, 255));
        approved_bttn2.setText("APPROVE");
        approved_bttn2.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                approved_bttn2ActionPerformed(evt);
            }
        });
        two_panel.add(approved_bttn2, new org.netbeans.lib.awtextra.AbsoluteConstraints(570, 350, 157, 33));

        decline_bttn.setBackground(new java.awt.Color(0, 51, 153));
        decline_bttn.setFont(new java.awt.Font("BankGothic Lt BT", 1, 14)); // NOI18N
        decline_bttn.setForeground(new java.awt.Color(255, 255, 255));
        decline_bttn.setText("DECLINE");
        decline_bttn.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                decline_bttnActionPerformed(evt);
            }
        });
        two_panel.add(decline_bttn, new org.netbeans.lib.awtextra.AbsoluteConstraints(160, 350, 157, 33));

        jtabbedpane1.addTab("APPROVAL", two_panel);

        javax.swing.GroupLayout jPanel5Layout = new javax.swing.GroupLayout(jPanel5);
        jPanel5.setLayout(jPanel5Layout);
        jPanel5Layout.setHorizontalGroup(
            jPanel5Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 900, Short.MAX_VALUE)
        );
        jPanel5Layout.setVerticalGroup(
            jPanel5Layout.createParallelGroup(javax.swing.GroupLayout.Alignment.LEADING)
            .addGap(0, 435, Short.MAX_VALUE)
        );

        jtabbedpane1.addTab("NOTIFICATIONS", jPanel5);

        getContentPane().add(jtabbedpane1, new org.netbeans.lib.awtextra.AbsoluteConstraints(150, 130, 900, 470));

        back_bttn.setFont(new java.awt.Font("BankGothic Lt BT", 1, 14)); // NOI18N
        back_bttn.setForeground(new java.awt.Color(0, 51, 153));
        back_bttn.setText("BACK");
        back_bttn.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                back_bttnActionPerformed(evt);
            }
        });
        getContentPane().add(back_bttn, new org.netbeans.lib.awtextra.AbsoluteConstraints(480, 630, 190, 40));

        jLabel1.setIcon(new javax.swing.ImageIcon("C:\\Users\\Yvette Pendel\\Pictures\\4.png")); // NOI18N
        jLabel1.setText("jLabel1");
        getContentPane().add(jLabel1, new org.netbeans.lib.awtextra.AbsoluteConstraints(0, 0, -1, -1));

        jMenu1.setForeground(new java.awt.Color(212, 175, 55));
        jMenu1.setText("TITLE");
        jMenuBar1.add(jMenu1);

        jMenu2.setForeground(new java.awt.Color(212, 175, 55));
        jMenu2.setText("COINS MULTIPLY DREAMS AMPLIFY");
        jMenuBar1.add(jMenu2);

        setJMenuBar(jMenuBar1);

        pack();
    }// </editor-fold>                        


    
    private void back_bttnActionPerformed(java.awt.event.ActionEvent evt) {                                          
        homepage Info = new homepage();
        Info.setVisible(true);
        this.dispose();        
    }                                         

    private void decline_bttnActionPerformed(java.awt.event.ActionEvent evt) {                                             
        try {
            updateAccountStatus("Declined");
        } catch (IOException ex) {
            Logger.getLogger(two.class.getName()).log(Level.SEVERE, null, ex);
        }
        
    }                                            

    private void approved_bttn2ActionPerformed(java.awt.event.ActionEvent evt) {                                               
        try {
            updateAccountStatus("Approved");
        } catch (IOException ex) {
            Logger.getLogger(two.class.getName()).log(Level.SEVERE, null, ex);
        }
    }                                              
     private void loadUserData() {
        DefaultTableModel model = (DefaultTableModel) listofusertable.getModel();
        loadUserInfo("user.csv", "USER", model);
    }
  private void loadUserInfo(String filePath, String role, DefaultTableModel model) {
        try (BufferedReader br = new BufferedReader(new FileReader(filePath))) {
            String line;
            while ((line = br.readLine()) != null) {
                String[] userInfo = line.split(",");
                if (userInfo.length == 2) {
                    model.addRow(new Object[]{userInfo[0], userInfo[1], role});
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    public static void main(String args[]) {
        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException | InstantiationException | IllegalAccessException | javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(two.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }

        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new two().setVisible(true);
            }
        });
    }

    private void updateAccountStatus(String status) throws IOException {
        
        int selectedRow = listofusertable.getSelectedRow();
        String accountNumber = listofusertable.getValueAt(listofusertable.getSelectedRow(), 1).toString();
        
        if (selectedRow != -1) {
            DefaultTableModel model = (DefaultTableModel) listofusertable.getModel();
            
            if(status.equals("Approved")) {
                try {
                // transfer the file into a temporary file
                BufferedReader reader = new BufferedReader(new FileReader("user.csv"));
                PrintWriter writer = new PrintWriter(new FileWriter("TemporaryFile.csv"));
                String line;
                
                while((line = reader.readLine()) != null) {
                    String[] accountDetails = line.split(",");
                    
                    writer.append(String.format("%s,%s,%s,%s,%s,%s,%s,%s\n",
                            accountDetails[0],
                            accountDetails[1],
                            accountDetails[2],
                            accountDetails[3],
                            accountDetails[4],
                            accountDetails[5],
                            accountDetails[6],
                            accountDetails[7]
                            ));
                }
                
//                reader.close();
                writer.close();
                
            } catch (FileNotFoundException ex) {
                Logger.getLogger(two.class.getName()).log(Level.SEVERE, null, ex);
            }
            
            // transfer the data from the temporary file into the original file
            try {
                BufferedReader reader = new BufferedReader(new FileReader("TemporaryFile.csv"));
                PrintWriter writer = new PrintWriter(new FileWriter("user.csv"));
                String line;
                
                while((line = reader.readLine()) != null) {
                    String[] accountDetails = line.split(",");
                    
                    // search for the specific account
                    if (!accountDetails[5].equals(accountNumber)) {
                        // if not the specific record, just copy it
                        writer.append(String.format("%s,%s,%s,%s,%s,%s,%s,%s\n",
                                accountDetails[0],
                                accountDetails[1],
                                accountDetails[2],
                                accountDetails[3],
                                accountDetails[4],
                                accountDetails[5],
                                accountDetails[6],
                                accountDetails[7]
                                ));
                    }
                    else {
                        writer.append(String.format("%s,%s,%s,%s,%s,%s,%s,APPROVED\n",
                                accountDetails[0],
                                accountDetails[1],
                                accountDetails[2],
                                accountDetails[3],
                                accountDetails[4],
                                accountDetails[5],
                                accountDetails[6]
                                ));
                    }
                }
                
                writer.close();
                reader.close();
                
            } catch (FileNotFoundException ex) {
                Logger.getLogger(two.class.getName()).log(Level.SEVERE, null, ex);
            }
            }
            else {
                try {
                // transfer the file into a temporary file
                BufferedReader reader = new BufferedReader(new FileReader("user.csv"));
                PrintWriter writer = new PrintWriter(new FileWriter("TemporaryFile.csv"));
                String line;
                
                while((line = reader.readLine()) != null) {
                    String[] accountDetails = line.split(",");
                    
                    writer.append(String.format("%s,%s,%s,%s,%s,%s,%s,%s\n",
                            accountDetails[0],
                            accountDetails[1],
                            accountDetails[2],
                            accountDetails[3],
                            accountDetails[4],
                            accountDetails[5],
                            accountDetails[6],
                            accountDetails[7]
                            ));
                }
                
//                reader.close();
                writer.close();
                
            } catch (FileNotFoundException ex) {
                Logger.getLogger(two.class.getName()).log(Level.SEVERE, null, ex);
            }
            
            // transfer the data from the temporary file into the original file
            try {
                BufferedReader reader = new BufferedReader(new FileReader("TemporaryFile.csv"));
                PrintWriter writer = new PrintWriter(new FileWriter("user.csv"));
                String line;
                
                while((line = reader.readLine()) != null) {
                    String[] accountDetails = line.split(",");
                    
                    // search for the specific account
                    if (!accountDetails[5].equals(accountNumber)) {
                        // if not the specific record, just copy it
                        writer.append(String.format("%s,%s,%s,%s,%s,%s,%s,%s\n",
                                accountDetails[0],
                                accountDetails[1],
                                accountDetails[2],
                                accountDetails[3],
                                accountDetails[4],
                                accountDetails[5],
                                accountDetails[6],
                                accountDetails[7]
                                ));
                    }
                    else {
                        writer.append(String.format("%s,%s,%s,%s,%s,%s,%s,DECLINED\n",
                                accountDetails[0],
                                accountDetails[1],
                                accountDetails[2],
                                accountDetails[3],
                                accountDetails[4],
                                accountDetails[5],
                                accountDetails[6]
                                ));
                    }
                }
                
                writer.close();
                reader.close();
                
            } catch (FileNotFoundException ex) {
                Logger.getLogger(two.class.getName()).log(Level.SEVERE, null, ex);
            }
            }
            
            
            
        } else {
            JOptionPane.showMessageDialog(this, "Please select a row to update.", "Error", JOptionPane.ERROR_MESSAGE);
        }
        
        // updates the data in the table
        displayAccountsForApproval();
    }

    private void writeUpdatedDataToCSV(String filePath) {
        DefaultTableModel model = (DefaultTableModel) listofusertable.getModel();
        try (BufferedWriter bw = new BufferedWriter(new FileWriter(filePath))) {
            for (int i = 0; i < model.getRowCount(); i++) {
                for (int j = 0; j < model.getColumnCount(); j++) {
                    bw.write(model.getValueAt(i, j).toString());
                    if (j < model.getColumnCount() - 1) {
                        bw.write(",");
                    }
                }
                bw.newLine();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton approved_bttn2;
    private javax.swing.JButton back_bttn;
    private javax.swing.JButton decline_bttn;
    private javax.swing.JInternalFrame jInternalFrame1;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JMenu jMenu1;
    private javax.swing.JMenu jMenu2;
    private javax.swing.JMenuBar jMenuBar1;
    private javax.swing.JPanel jPanel5;
    private javax.swing.JScrollPane jScrollPane1;
    private javax.swing.JTabbedPane jtabbedpane1;
    private javax.swing.JTable listofusertable;
    private javax.swing.JPanel two_panel;
    // End of variables declaration                   
}
