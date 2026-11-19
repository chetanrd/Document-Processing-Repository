# Contributing to document-processing-toolkit

Thank you for considering a contribution! This is an early-stage open-source project and all help is appreciated.

## Ways to Contribute

- **Bug reports** — File an issue with steps to reproduce
- **Feature requests** — Suggest new functionality
- **Code contributions** — Submit pull requests
- **Documentation** — Improve README, add examples
- **Testing** — Add test cases, report edge cases

## Development Setup

```bash
git clone https://github.com/your-username/document-processing-toolkit.git
cd document-processing-toolkit
pip install -e .[dev]
```

## Running Tests

```bash
pytest
# or
python -m pytest tests/ -v
```

## Code Style

- Follow PEP 8
- Type hints encouraged for new code
- Keep functions small and focused
- Use standard library where possible

## Pull Request Process

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Make your changes
4. Run tests (`pytest`)
5. Ensure new code has test coverage
6. Submit a pull request

## Adding New File Format Support

To add support for a new file format:

1. Add the extension to `SUPPORTED_TEXT_EXTENSIONS` in `core.py`
2. Add an extraction function (e.g., `_extract_docx`)
3. Update `extract_text()` to dispatch to the new function
4. Add the dependency to `requirements.txt` and `pyproject.toml`
5. Add tests in `tests/test_core.py`
6. Update the README with the new format

## Reporting Security Issues

Please do not file public issues for security vulnerabilities. Instead, email the maintainers directly.

## Code of Conduct

Be respectful and inclusive. Harassment of any kind will not be tolerated.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.