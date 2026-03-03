

## Persistência de Progresso do Formulário

### Problema
Ao sair da página ou recarregar, todo o progresso do formulário é perdido.

### Solução
Salvar automaticamente o estado do formulário no `localStorage` do navegador, incluindo:
- Tipo de negócio selecionado (`businessType`)
- Etapa atual (`currentStepIndex`)
- Dados do formulário profissional (`formData`)
- Dados do formulário contábil (`acctFormData`)

### Implementação

**Arquivo: `src/components/form/MultiStepForm.tsx`**

1. **Carregar estado salvo na inicialização** — usar `useState` com initializer functions que leem do `localStorage`.

2. **Salvar automaticamente a cada mudança** — adicionar um `useEffect` que observa `businessType`, `currentStepIndex`, `formData` e `acctFormData`, gravando no `localStorage` com uma chave como `kenkya-form-progress`.

3. **Limpar ao enviar ou resetar** — no `handleSubmit` (após sucesso) e no `handleReset`, chamar `localStorage.removeItem('kenkya-form-progress')`.

Estrutura salva:
```text
localStorage['kenkya-form-progress'] = JSON.stringify({
  businessType,
  currentStepIndex,
  formData,
  acctFormData
})
```

Nenhuma mudança no banco de dados é necessária — tudo fica local no navegador do usuário.

