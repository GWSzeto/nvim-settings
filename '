local cmp = require("cmp")
local luasnip = require("luasnip")

local function has_words_before()
    local line, col = unpack(vim.api.nvim_win_get_cursor(0))
    return col ~= 0 and vim.api.nvim_buf_get_lines(0, line - 1, line, true)[1]:sub(col, col):match("%s") == nil
end

cmp.setup({
    mapping = {
        ["<Tab>"] = cmp.mapping(function(fallback)
            if require("copilot.suggestion").is_visible() then
                require("copilot.suggestion").accept()
            elseif cmp.visible() then
                cmp.select_next_item({ behavior = cmp.SelectBehavior.Insert })
            elseif luasnip.expandable() then
                luasnip.expand()
            elseif has_words_before() then
                cmp.complete()
            else
                fallback()
            end
        end, {
        "i",
        "s",
    }),
},
})
