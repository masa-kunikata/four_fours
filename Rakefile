require 'yaml'
task default: :four_four 

F = '4.0'

PARENS = [
# [nil, F,   nil, aop, nil, F,   nil, bop, nil, F,   nil, cop, nil, F,   nil]
  ['(', nil, nil, nil, nil, nil, ')', nil, nil, nil, nil, nil, nil, nil, nil],
  ['(', nil, nil, nil, nil, nil, nil, nil, nil, nil, ')', nil, nil, nil, nil],
  ['(', nil, nil, nil, nil, nil, ')', nil, '(', nil, nil, nil, nil, nil, ')'],
  [nil, nil, nil, nil, '(', nil, nil, nil, nil, nil, ')', nil, nil, nil, nil],
  [nil, nil, nil, nil, '(', nil, nil, nil, nil, nil, nil, nil, nil, nil, ')'],
  [nil, nil, nil, nil, nil, nil, nil, nil, '(', nil, nil, nil, nil, nil, ')'],
]

desc 'the task'
task :four_four do
  equations = {}

  operators = %w[+ - / *]

  operators.each do |aop|
    operators.each do |bop|
      operators.each do |cop|
        elems = [nil, F, nil, aop, nil, F, nil, bop, nil, F, nil, cop, nil, F, nil]
        PARENS.each do |parens|
          strs = elems.zip(parens).map do |e, p|
            e || p || ''
          end
          q = strs.join
          a = eval(q) rescue nil
          # puts q, a
          equations[a] = [] unless equations[a]
          arr = equations[a]
          arr << q
        end
      end
    end
  end

  jp_eqs = (0..10).map do |ans|
    hit_eqs = equations[ans.to_f]
    int_eqs = hit_eqs&.map do |s|
      s.gsub('.0', '').tr('\(\)/4\+\-\*', '（）÷４＋－×')
    end
    [ans, int_eqs]
  end.to_h

  File.write('answers.yaml', jp_eqs.to_yaml)
end

