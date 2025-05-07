# ProjetoForms1.FrmLogin
Logotipo de login

using System;
using System.Data.SqlClient;
using System.Drawing;
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

// Verificação local (hardcoded)
            if (usuario == "admin" && senha == "1234")
            {
                lblStatus.ForeColor = Color.Green;
                lblStatus.Text = "Login bem-sucedido!";
                MessageBox.Show("Login como administrador!", "Sucesso", MessageBoxButtons.OK, MessageBoxIcon.Information);

// Exemplo: abrir formulário principal
                FrmMenu mainForm = new FrmMenu();
                mainForm.Show();
                this.Hide();
                return;
            }

// Verificação com banco de dados
            string connectionString = "sua_string_de_conexao"; // Substitua pela sua string de conexão real
            string query = "SELECT COUNT(*) FROM funcionario WHERE usuario = @usuario AND senha = @senha";

try
            {
                using (SqlConnection conn = new SqlConnection(connectionString))
                using (SqlCommand cmd = new SqlCommand(query, conn))
                {
                    cmd.Parameters.AddWithValue("@usuario", usuario);
                    cmd.Parameters.AddWithValue("@senha", senha);

conn.Open();
                    int count = (int)cmd.ExecuteScalar();

if (count > 0)
                    {
                        lblStatus.ForeColor = Color.Green;
                        lblStatus.Text = "Login bem-sucedido!";
                        MessageBox.Show("Login realizado com sucesso!", "Sucesso", MessageBoxButtons.OK, MessageBoxIcon.Information);

FrmMenu mainForm = new FrmMenu();
                        mainForm.Show();
                        this.Hide();
                    }
                    else
                    {
                        lblStatus.ForeColor = Color.Red;
                        lblStatus.Text = "Usuário ou senha incorretos!";
                        txtSenha.Clear();
                        txtSenha.Focus();
                    }
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show($"Erro durante a autenticação:\n{ex.Message}", "Erro", MessageBoxButtons.OK, MessageBoxIcon.Error);
                lblStatus.ForeColor = Color.Red;
                lblStatus.Text = "Erro durante a autenticação!";
                txtSenha.Clear();
                txtSenha.Focus();
            }
        }

private void btnLimpar_Click(object sender, EventArgs e)
        {
            txtLogin.Clear();
            txtSenha.Clear();
            lblStatus.Text = "*";
            lblStatus.ForeColor = Color.Black;
            txtLogin.Focus();
        }
    }
}
