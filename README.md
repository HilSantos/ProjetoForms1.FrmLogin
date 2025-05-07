# ProjetoForms1.FrmLogin
Logotipo de login

using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;


namespace ProjetoForms1
    {
        public partial class FrmLogin : Form
        {
            public FrmLogin()
            {
                InitializeComponent();
            }

private void FrmLogin_Load(object sender, EventArgs e)
            {
                txtLogin.Focus();
                lblStatus.Text = "*";
            }

private void btnEntrar_Click(object sender, EventArgs e)
            {
                string usuario = txtLogin.Text.Trim();
                string senha = txtSenha.Text;

if (usuario == "admin" && senha == "1234")
                {
                    lblStatus.ForeColor = System.Drawing.Color.Green;
                    lblStatus.Text = "Login bem-sucedido!";

// Aqui você pode abrir outro formulário, se quiser
                    // Por exemplo:
                    // FrmPrincipal frm = new FrmPrincipal();
                    // frm.Show();
                    // this.Hide();
                }
                    string query = "SELECT COUNT(*) FROM funcionario WHERE" + "usuario = @usuario AND senha = " +
    "@senha";
using (SqlConnection conn = new SqlConnection("sua_string_de_conexao"))
{
    SqlCommand cmd = new SqlCommand(query, conn);
    cmd.Parameters.AddWithValue("@usuario", usuario);
    cmd.Parameters.AddWithValue("@senha", senha);
    conn.Open();
    int count = (int)cmd.ExecuteScalar();
    if (count > 0)
    {
        // Login bem-sucedido
        MessageBox.Show("Login bem-sucedido!");
    }
        else
        {
            // Login falhou
            MessageBox.Show("Usuário ou senha incorretos!");
        }
    }
}
    
else
                {
                    lblStatus.ForeColor = System.Drawing.Color.Red;
                    lblStatus.Text = "Usuário ou senha incorretos!";
                    txtSenha.Clear();
                    txtSenha.Focus();
                }
            }

private void btnLimpar_Click(object sender, EventArgs e)
            {
                txtLogin.Clear();
                txtSenha.Clear();
                lblStatus.Text = "*";
                lblStatus.ForeColor = System.Drawing.Color.Black;
                txtLogin.Focus();
            }
        }
    }
