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
